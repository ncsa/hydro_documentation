.. _quick:

Quick Start Guide
==================

This information is for users that are adept at using an HPC system and are only interested in the basic Hydro workflow.

- :ref:`access-and-policy`: Access to Hydro is limited to `New Frontiers Initiative <https://newfrontiers.illinois.edu/about/>`_ (NFI) projects and `Illinois Computes <https://computes.illinois.edu>`_ projects that need access to the Hydro compute resource.

- :ref:`logging-in`: Access Hydro through SSH with `NCSA Duo <https://wiki.ncsa.illinois.edu/display/cybersec/Duo+at+NCSA>`_ authentication. For example, ``ssh hydro.ncsa.illinois.edu``.

- :ref:`compiling`: Compile MPI code, and automatically include OpenMPI libraries, with compiler wrappers. For example, ``mpicc -o foo.exe foo.c``.

- :ref:`running`: Hydro uses `Slurm <https://slurm.schedmd.com/documentation.html>`_ to run jobs. Use ``sbatch`` or ``srun``, as appropriate, to submit a job to a queue. For example, ``srun -n 1 ./foo.exe``. A :ref:`sample batch script <sample-batch-script>` is also available.

- :ref:`partitions-job-policies`: See the :ref:`partitions <partitions-job-policies>` and :ref:`architecture <architecture>` sections for the name and technical details of Hydro's queues. 

- Track project usage with the ``accounts`` or ``accounts-remaining`` command, depending on your project's :ref:`charging policy <project-job-accounting>`.
