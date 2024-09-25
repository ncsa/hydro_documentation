.. _prog_env:

Programming Environments
=========================

.. _software:

Software
-------------

- Red Hat Enterprise Linux (RHEL) `8.4 <https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/8.4_release_notes/index>`_
- Linux Kernel 4.18.0
- Software is installed using `Spack <https://spack.io>`_
      
  - OpenMPI
  - FFTW
  - Python (and TensorFlow)
  - GCC 11.3.0
  - R
  - GDAL
  - AWS CLI
  - Run ``module avail`` on the Hydro login node for a complete list of installed software.

.. _shells-modules:

Shells and Modules
---------------------------

The default shell is **/bin/bash**. To request it be changed, :ref:`submit a support request <help>`. 

The user environment is controlled using the modules environment management system. 
Modules may be loaded, unloaded, or swapped either on a command line or in your **$HOME/.bashrc** (**.cshrc** for csh ) shell startup file.

The ``module`` command is a user interface to the Lmod package. 
The `Lmod package <https://lmod.readthedocs.io/en/latest/010_user.html>`_ provides for the dynamic modification of the user’s environment via **modulefiles** (a modulefile contains the information needed to configure the shell for an application). 
Modules are independent of the user’s shell, so both **tcsh** and **bash** users can use the same commands to change the environment.

.. table:: Useful Module Commands

   =========================================== ==========================
   Command                                     Description                      
   =========================================== ==========================
   ``module avail``                            lists all available modules      
   ``module list``                             lists currently loaded modules
   ``module avail | more``		           display the available modules on the system one page at a time
   ``module spider foo``                       search for modules named **foo**     
   ``module help modulefile``                  help on module **modulefile**        
   ``module display modulefile``               display information about **modulefile**      
   ``module load modulefile``                  load **modulefile** into current shell environment     
   ``module unload modulefile``                remove **modulefile** from current shell environment  
   ``module swap modulefile1 modulefile2``     unload **modulefile1** and load **modulefile2**  
   =========================================== ==========================

**To include a particular software stack in your default environment for Hydro login and compute nodes:**

  #. Log into a Hydro login node. 
  #. Manipulate your modulefile stack until satisfied. 
  #. Run ``module save``; this will create a **.lmod.d/default** file that will be loaded on the Hydro login or compute nodes on your next login or job execution.

.. table:: Useful User Defined Module Collections

   ==================================== =======================
   Command                              Description                      
   ==================================== =======================
   ``module save``                      save current modulefile stack to **~/.lmod.d/default** 
   ``module save collection_name``      save current modulefile stack to **~/.lmod.d/collection_name**
   ``module restore``                   load **~/.lmod.d/default** if it exists or System default    
   ``module restore collection_name``   load your **~/.lmod.d/collection_name**                       
   ``module reset``                     reset your modulefiles to System default 
   ``module disable collection_name``   disable **collection_name** by adding **collection_name~**      
   ``module savelist``                  list all your **~/.lmod.d/collections**                   
   ``module describe collection_name``  list **collection_name modulefiles** 
   ==================================== =======================


Programming Environments
------------------------------

The `GNU Compiler Collection (GCC) <https://gcc.gnu.org>`_ version 11.3.0 is in the default user environment. 

.. _compiling:

Compiling
------------

To compile MPI code, use the ``mpicc``, ``mpiCC``, or ``mpif90`` compiler wrappers to automatically include the OpenMPI libraries.

For example:

.. code-block::

   mpicc -o mpi_hello mpi_hello.c

If the code also uses OpenMP, include the **-fopenmp** flag:

.. code-block::

   mpicc -o omp_mpi_hello omp_mpi_hello.c -fopenmp


Other Programming Environments
--------------------------------

.. _python:

Python
---------

If you want a basic, recent Python setup, use the ``python`` installation under the ``gcc`` module. You can add modules via ``pip3 install --user <modulename>``, setup virtual environments, and customize as needed for your workflow but starting from a smaller installed base of Python than Anaconda.

.. code-block::

   $ module load gcc python
   $ which python
   /sw/spack/hydrogpu-2022-06/apps/python/3.9.13-gcc-11.3.0-jkmnqio/bin/python
   $ module list

   Currently Loaded Modules:
     1) modtree/gpu            3) user/license_file   5) gcc/11.3.0    7) openmpi/4.1.4
     2) scripts/script_paths   4) StdEnv              6) cuda/11.7.0   8) python/3.9.13

View the python packages installed in this environment using ``pip3 list``

Anaconda
--------

The Anaconda Python distribution is also available on Hydro by loading either the ``anaconda3_cpu`` or ``anaconda3_gpu`` module. Anaconda comes with many included Python packages and uses the `Conda package manager <https://docs.conda.io/en/latest/>`_ for viewing and installing packages. 

anaconda3_cpu
---------------

Use Python from the ``anaconda3_cpu`` module if you need some of the modules provided by Anaconda in your Python workflow.  For GPU nodes, use ``anaconda3_gpu``.

.. code-block::

   $ module load modtree/cpu

   Due to MODULEPATH changes, the following have been reloaded:
     1) gcc/11.3.0     2) openmpi/4.1.4

   The following have been reloaded with a version change:
     1) modtree/gpu => modtree/cpu

   $ module load gcc anaconda3_cpu
   $ which conda
   /sw/external/python/anaconda3_cpu/bin/conda
   $ module list

   Currently Loaded Modules:
     1) scripts/script_paths   3) StdEnv        5) gcc/11.3.0      7) anaconda3_cpu/4.13.0
     2) user/license_file      4) modtree/cpu   6) openmpi/4.1.4

Use the ``conda list`` command to view the list of modules available in ``anaconda3_cpu``.

anaconda3_gpu (for CUDA)
------------------------

Like the setup for ``anaconda_cpu``, Hydro has GPU versions of anaconda3 (``module load anaconda3_gpu``) and there are PyTorch and TensorFlow CUDA-aware Python modules installed into these versions.  You may use these modules when working with the GPU nodes. See ``conda list`` after loading the module to review what is already installed. As with ``anaconda3_cpu``, let Hydro staff know if there are modules you would like installed for the broader community by :ref:`submitting a support request <help>`.

Installing packages
-------------------- 

On Hydro, you can install your own Python software stacks, as needed. There are a couple of choices when customizing your Python setup.  You may use any of these methods with any of the Python versions or instances described below (or you may install your own Python versions):

- **pip3** (Python module or Anaconda): ``pip3 install --user <python_package>``

  Useful when you need just one Python environment per Python version or instance.

- **venv** python virtual environment (Python module or Anaconda):

  Can name environments (metadata) and have multiple environments per Python version or instance.

- **conda environments** (Anaconda only)

  Like ``venv`` but with more flexibility. See the `Managing Environments section of the Conda getting started guide <https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html>`_ to learn how to customize Conda for your workflow and add extra python modules to your environment.

|
