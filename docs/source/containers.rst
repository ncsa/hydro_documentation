Containers
==============

Containerization is a modern software packaging and execution technology that
allows scripts and executables to be distributed with not only libraries and
other dependencies, but a complete Linux operating system environment.
Unlike virtual machines, which run a separate kernel on virtual processors,
containerized applications share the same kernel as the host
and therefore suffer practically no overhead.

The Hydro cluster supports containers via `Apptainer <https://apptainer.org/>`_
(formerly Singularity),
which is similar to Docker but specialized for traditional HPC environments.
Apptainer distinguishes itself in that root/sudo authorization is not required
to either run or (as of version 1.1) build containers (technical details at
https://arxiv.org/ftp/arxiv/papers/2208/2208.12106.pdf).

Apptainer 1.1 is installed on all Hydro login and compute nodes
at /usr/bin/apptainer and is fully documented at https://apptainer.org/docs/user/1.1/
so the following is limited to details and advice specific to Hydro.


Using Docker Images with Apptainer
---------------------------------------

**Option 1 - Just run it:**
::

   apptainer run docker://rockylinux:8

Images are cached in $APPTAINER_CACHEDIR if set,
or in $HOME/.apptainer/cache by default.

**Option 2 - Download to Singularity Image Format (SIF) file and run:**
::

   apptainer pull docker://rockylinux:8

   apptainer run rockylinux_8.sif

A SIF file can also be run directly (assuming execute permission):
::

   ./rockylinux_8.sif

**Option 3 - Download to local sandbox directory and modify:**
::

   apptainer build --sandbox /tmp/rocky docker://rockylinux:8

   apptainer exec --fakeroot --writable /tmp/rocky yum install -y which

   apptainer run --fakeroot --writable /tmp/rocky

You can test the sandbox as a normal user in read-only mode:
::

   apptainer run /tmp/rocky

The Lustre home and projects filesystems lack xattr support,
which results in a long stream of error messages from apptainer build
and causes yum install transaction failures.
It is therefore necessary to use a writable local filesystem (/tmp)
for sandboxes, and then convert the image to a SIF file on a cross-node
filesystem for future use, e.g.:
::

   apptainer build --fakeroot newrocky.sif /tmp/rocky

**Option 4 - Convert Dockerfile to Apptainer definition file and build:**

`Singularity Python <https://singularityhub.github.io/singularity-cli/>`_
provides a `recipe converter <https://singularityhub.github.io/singularity-cli/recipes>`_
from Dockerfile format to `Apptainer definition file format
<https://apptainer.org/docs/user/1.1/definition_files.html>`_.
The converter greatly simplifies the process but isn't perfect,
particularly when files are copied using relative paths.
::

   pip3 install spython --user

   spython recipe Dockerfile image.def

   apptainer build image.sif image.def


Interacting with Host Filesystems
--------------------------------------

Apptainer will bind-mount $HOME and /tmp into the container by default.
Additional directories may be mounted with ``--bind src[:dest[:ro]]``
and default mounts suppressed with ``--no-home`` or ``--contain``.
The caller's current user and group will appear unchanged,
but all other users and groups will appear as nobody.
(With the ``--fakeroot`` option $HOME will be mounted as /root
and the caller's user and group will be mapped to root.)
Regardless of apparent user and group, **processes inside a
container have the caller's full read and write capabilities
on mounted host filesystems.**

See https://apptainer.org/docs/user/1.1/bind_paths_and_mounts.html for details.


Mounting Images of Many-File Datasets
----------------------------------------

Shared network filesystems, such as Lustre used for home and projects,
incur much higher latencies opening and closing files than local filesystems do.
For this reason, workflows that process many small files can
run orders of magnitude slower on a cluster than on a desktop workstation.

As described at https://apptainer.org/docs/user/1.1/bind_paths_and_mounts.html#image-mounts,
Apptainer can bind-mount image files in standard ext3 and squashfs formats
as well as its own SIF format.
An image file can contain millions of tiny files while
providing the simplicity and performance of a single large file.
Each image file can safely be mounted either read-write by a single container
or read-only by many containers (but not both at the same time).


Running with GPU Acceleration
-------------------------------

Apptainer GPU support is described in detail at
https://apptainer.org/docs/user/1.1/gpu.html,
but adding ``--nv`` should just work, assuming that
GPUs were correctly requested in the Slurm submission options.
Devices visible with nvidia-smi outside a container
should be visible inside a container launched with ``--nv``.


Running on Multiple Nodes with MPI
-----------------------------------

The many limitations and pitfalls of combining containers and MPI
are detailed at https://apptainer.org/docs/user/1.1/mpi.html
but the short story is that the MPI library used inside the container
must be compatible with both the host mpiexec or srun program
used to launch the container and with the host high-speed network.
Images based on the latest OpenMPI release seem likely to work.

The `NVIDIA GPU Cloud (NGC) HPC benchmark
<https://catalog.ngc.nvidia.com/orgs/nvidia/containers/hpc-benchmarks>`_ 
HPL image can be launched within a Slurm job by:
::

  srun --mpi=pmi2 --cpu-bind=none apptainer run --nv NGC/hpc-benchmarks\:21.4-hpl hpl.sh ...

The job script sets all the node counts, task counts etc.
but the hpl.sh script uses numactl so both cpu and gpu binding must be disabled.
The ``--mpi=pmi2`` option overrides Hydro's default pmix, but if there is a failure
the pmi signal handling doesn’t work and the run hangs rather than exits.

The `Extreme-scale Scientific Software Stack (E4S) <https://e4s-project.github.io/>`_
image just works out of the box.
The image is 40 GB, so the box is pretty big, but "spack list" shows over 6,000 packages
that you can "spack load" (and in some cases "module load")
to run directly or to build into your own program on a host filesystem.
MPI applications can be launched inside the container by:
::

  mpiexec ... apptainer exec e4s-cuda-x86_64-22.08.sif myprog ...

While the ``--cleanenv`` option can prevent interaction with the Hydro module system
when building software, in a parallel job it blocks environment variables needed by MPI,
resulting in many independent processes rather than a single unified MPI launch.

Accessing Hydro Modules in a Container
----------------------------------------

The following Apptainer definition file will build an image
that is compatible with the Hydro base OS and modules,
including the MPI library, if launched with the ``--bind`` and
``--env`` options shown in the %help section.
The definition file can be extended to yum install additional
packages to augment the Hydro software stack
when building and running software in a container.
::

   Bootstrap: docker
   From: rockylinux:8

   %post

   # for Lmod
   yum install -y lua
   yum install -y epel-release
   /usr/bin/crb enable
   yum repolist
   yum install -y Lmod

   # useful
   yum install -y which
   yum install -y make
   yum install -y findutils
   yum install -y glibc-headers
   yum install -y glibc-devel
   yum install -y tcl-devel

   # for MPI
   yum install -y hwloc-libs
   yum install -y ucx
   yum install -y libevent

   # for GDAL
   yum install -y libtiff
   yum install -y libpng

   %help

   Enables host modules and MPI in container.

   Recommended apptainer launch options are:
     --bind /sw \
     --bind /usr/lib64/liblustreapi.so.1 \
     --bind /usr/lib64/libpmix.so.2 \
     --bind /usr/lib64/pmix \
     --env PREPEND_PATH="$PATH" \
     --env LD_LIBRARY_PATH="$LD_LIBRARY_PATH"

   Should work with GPUs if --nv added.


