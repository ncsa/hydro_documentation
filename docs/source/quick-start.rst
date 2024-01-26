.. _quick:

Quick Start Guide
==================

This information is for users that are adept at using an HPC system and are only interested in the basic Hydro workflow.

- :ref:`Access to Hydro <access-and-policy>` is limited to `New Frontiers Initiative <https://newfrontiers.illinois.edu/about/>`_ (NFI) projects and `Illinois Computes <https://computes.illinois.edu>`_ projects that need access to the Hydro compute resource.

..

- :ref:`Log into Hydro <logging-in>` through SSH with `NCSA Duo <https://wiki.ncsa.illinois.edu/display/cybersec/Duo+at+NCSA>`_ authentication. 

  .. code-block:: terminal

     ssh hydro.ncsa.illinois.edu

..

- :ref:`Compile <compiling>` MPI code, and automatically include OpenMPI libraries, with compiler wrappers. For example, ``mpicc -o foo.exe foo.c``.

..

- :ref:`Run jobs on Hydro <running>` with `Slurm <https://slurm.schedmd.com/documentation.html>`_. Use ``sbatch`` or ``srun`` to submit a job to a queue. For example, ``srun -n 1 ./foo.exe``; a :ref:`sample batch script <sample-batch-script>` is also available.

..

- The :ref:`Partitions <partitions-job-policies>` and :ref:`Architecture <architecture>` sections include the name and technical details of Hydro's queues. 

..

- :ref:`Track project usage <project-job-accounting>` with the ``accounts`` command (for projects charged monthly) or the ``accounts-remaining`` command (for projects with fixed allocations).

..

- :ref:`Transfer files <globus>` with `Globus <https://www.globus.org>`_ (endpoint **NFI Hydro**), linked to your **NCSA identity**.

|
