.. _programming_environments:

Programming Environments
=========================

.. _software:

Software
-------------

-  RHEL 8.4
-  Kernel 4.18.0
-  Software

   -  Currently software is installed using Spack
   -  A complete list of installed software can be generated by the
      command ``module avail`` on the Hydro login node.
   -  A sample of select packages

      -  OpenMPI
      -  FFTW
      -  Python

         -  Tensorflow

      -  GCC 11.3.0
      -  R
      -  GDAL
      -  AWS CLI

.. _shells-and-modules:

Shells and Modules
---------------------------

The default shell is /bin/bash. You can change it by sending a request
via email to help+hydro@ncsa.illinois.edu. 

The user environment is controlled using the modules environment
management system. Modules may be loaded, unloaded, or swapped either on
a command line or in your $HOME/.bashrc (.cshrc for csh ) shell startup
file.

The command "*module avail \| more"* will display the available modules on
the system one page at a time.

The module command is a user interface to the Lmod package. The Lmod
package provides for the dynamic modification of the user’s environment
via *modulefiles* (a modulefile contains the information needed to
configure the shell for an application). Modules are independent of the
user’s shell, so both tcsh and bash users can use the same commands to
change the environment.

`Lmod User
Guide <https://lmod.readthedocs.io/en/latest/010_user.html>`__

Useful Module commands:

+----------------------------------+----------------------------------+
| Command                          | Description                      |
+==================================+==================================+
| module avail                     | lists all available modules      |
+----------------------------------+----------------------------------+
| module list                      | lists currently loaded modules   |
+----------------------------------+----------------------------------+
| module spider foo                | search for modules named foo     |
+----------------------------------+----------------------------------+
| module help *modulefile*         | help on module modulefile        |
+----------------------------------+----------------------------------+
| module display *modulefile*      | Display information about        |
|                                  | modulefile                       |
+----------------------------------+----------------------------------+
| module load *modulefile*         | load modulefile into current     |
|                                  | shell environment                |
+----------------------------------+----------------------------------+
| module unload *modulefile*       | remove modulefile from current   |
|                                  | shell environment                |
+----------------------------------+----------------------------------+
| module swap *modulefile1         | unload modulefile1 and load      |
| modulefile2*                     | modulefile2                      |
+----------------------------------+----------------------------------+

**To include a particular software stack in your default environment for
hydro login and computes**

Log into hydro login node, manipulate your modulefile stack until
satisfied. *module save;* This will create a .lmod.d/default file. It
will be loaded on hydro login or computes on next login or job
execution.

Useful User Defined Module Collections:

+----------------------------------+----------------------------------+
| Command                          | Description                      |
+==================================+==================================+
| module save                      | Save current modulefile stack to |
|                                  | ~/.lmod.d/default                |
+----------------------------------+----------------------------------+
| module save collection_name      | Save current modulefile stack to |
|                                  | ~/.lmod.d/collectioin_name       |
+----------------------------------+----------------------------------+
| module *restore*                 | Load ~/.lmod.d/default if it     |
|                                  | exists or System default         |
+----------------------------------+----------------------------------+
| module *restore collection_name* | Load your                        |
|                                  | ~/.lmod.d/collectioin_name       |
+----------------------------------+----------------------------------+
| module *reset*                   | Reset your modulefiles to System |
|                                  | default                          |
+----------------------------------+----------------------------------+
| module *disable collection_name* | Disable collection_name by       |
|                                  | adding collection_name~          |
+----------------------------------+----------------------------------+
| module *savelist*                | List all your                    |
|                                  | ~/.lmod.d/collections            |
+----------------------------------+----------------------------------+
| module describe collection_name  | List collection_name modulefiles |
+----------------------------------+----------------------------------+


Programming Environments
------------------------------

The GNU compilers (GCC) version 11.3.0 are in the default user
environment. 

.. _compiling:

Compiling
------------

| To compile MPI code, use the *mpicc, mpiCC, or mpif90* compiler
  wrappers to automatically include the OpenMPI libraries.
| For example:
| *mpicc -o mpi_hello mpi_hello.c*
| If the code also uses OpenMP, include the -fopenmp flag:
| *mpicc -o omp_mpi_hello omp_mpi_hello.c -fopenmp*


Other Programming Environments
--------------------------------
.. toctree::
   
   programming_environments/python