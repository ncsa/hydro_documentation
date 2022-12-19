.. _python:

======
Python
======

The default gcc (latest version) programming environment for either ``modtree/cpu`` or ``modtree/gpu`` contains:

Python
-----------------------------------
If you want a basic recent Python setup, use the python installation under the gcc module.  You can add modules via ``pip3 install --user <modulename>``,  setup virtual environments, and customize as needed for your workflow but starting from a smaller installed base of python than Anaconda.

::

  $ module load gcc python
  $ which python
  /sw/spack/hydrogpu-2022-06/apps/python/3.9.13-gcc-11.3.0-jkmnqio/bin/python
  $ module list

  Currently Loaded Modules:
    1) modtree/gpu            3) user/license_file   5) gcc/11.3.0    7) openmpi/4.1.4
    2) scripts/script_paths   4) StdEnv              6) cuda/11.7.0   8) python/3.9.13

You can view the python packages installed in this environment using ``pip3 list``

Anaconda
--------
The Anaconda Python distribution is also available on Hydro by loading either the ``anaconda3_cpu`` or ``anaconda3_gpu`` modules. Anaconda comes with many included Python packages, and also uses the conda pagakage manager for viewing and installing packages. 

anaconda3_cpu
---------------------------
Use python from the ``anaconda3_cpu`` module if you need some of the modules provided by Anaconda in your python workflow.  For GPU nodes, use ``anaconda3_gpu``.

::

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

The current list of modules available in anaconda3_cpu is shown via ``conda list``, including tensorflow, pytorch, etc.

anaconda3_gpu (for cuda)
------------------------
Similar to the setup for anaconda_cpu, we have gpu versions of anaconda3 (module load anaconda3_gpu) and have installed pytorch and tensorflow cuda-aware python modules into these versions.  You may use these module when working with the gpu nodes.  See conda list after loading the module to review what is already installed.  As with anaconda3_cpu, let Hydro staff know if there are generally useful modules you would like us to try to install for the broader community.

Installing packages
------------------- 
On Hydro, you may install your own python software stacks as needed.  There are a couple choices when customizing your python setup.  You may use any of these methods with any of the python versions or instances described below (or you may install your own python versions):

1. pip3 (Python module or Anaconda): ``pip3 install --user <python_package>``
	useful when you need just 1 python environment per python version or instance.
2. venv python virtual environment (Python module or Anaconda):
	can name environments (metadata) and have multiple environments per python version or instance
3. conda environments  (Anaconda only)
	similar to venv but with more flexibility. See the `Managing Environments <https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html>`_ section of the Conda getting started guide to learn how to customize Conda for your workflow and add extra python modules to your environment.
