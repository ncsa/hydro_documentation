.. _partitions-job-policies:

Partitions and Job Policies
===========================

This page lists job partitions, job limits, and QOS considerations for submitting jobs to the Hydro cluster.


Hydro Partitions (Queues)
--------------------------

.. table:: Hydro Partitions/Queues

   +-------------------+---------------+-----------+--------------+----------------+---------------+
   | Partition (Queue) | Node/Job Type | Max Nodes | Max Duration | Max Running in | Charge Factor |
   |                   |               |           |              |                |               |
   |                   |               | per Job   |              | Queue/user     |               |
   +===================+===============+===========+==============+================+===============+
   | sandybridge       | CPU (Intel)   | TBD       | 7 days       | TBD            | 1.0           |
   +-------------------+---------------+-----------+--------------+----------------+---------------+
   | sandybridge2.9    | CPU (Intel)   | TBD       | 7 days       | TBD            | 1.0           |
   +-------------------+---------------+-----------+--------------+----------------+---------------+
   | sandybridge2.0    | CPU (Intel)   | TBD       | 7 days       | TBD            | 1.0           |
   +-------------------+---------------+-----------+--------------+----------------+---------------+
   | interlagos        | CPU (AMD)     | TBD       | 7 days       | TBD            | 1.0           |
   +-------------------+---------------+-----------+--------------+----------------+---------------+
   | milan             | CPU (AMD)     | TBD       | 7 days       | TBD            | 6.0           |
   +-------------------+---------------+-----------+--------------+----------------+---------------+
   | rome              | CPU (AMD)     | TBD       | 7 days       | TBD            | 6.0           |
   +-------------------+---------------+-----------+--------------+----------------+---------------+
   | a100              | dual A100 GPU | TBD       | 7 days       | TBD            | 20.0          |
   |                   |               |           |              |                |               |
   |                   | w/ any CPU    |           |              |                |               |
   +-------------------+---------------+-----------+--------------+----------------+---------------+
   | a100milan         | dual A100 GPU | TBD       | 7 days       | TBD            | 20.0          |
   |                   |               |           |              |                |               |
   |                   | w/ Milan CPU  |           |              |                |               |
   +-------------------+---------------+-----------+--------------+----------------+---------------+
   | a100rome          | dual A100 GPU | TBD       | 7 days       | TBD            | 20.0          |
   |                   |               |           |              |                |               |
   |                   | w/ Rome CPU   |           |              |                |               |
   +-------------------+---------------+-----------+--------------+----------------+---------------+

- Sandybridge nodes have 16 cores per node, dual-socket, 384MB (2.9 and 2.0 ghz).
- Interlagos nodes have 64 cores per node, quad-socket, 512MB.
- Milan nodes have 56 cores per node, dual socket, 256MB.
- Rome nodes have 64 cores per node, dual socket, 256MB.

sview View of Slurm Partitions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Slurm's ``sview`` command provides a graphical view into a resource's partition and node properties.

Node Policies
~~~~~~~~~~~~~

Node-sharing is not enabled; jobs currently run exclusive. 

When node-sharing with jobs is enabled, node-exclusive mode can be obtained by specifying all the consumable resources for that node type or adding the following Slurm options:

   .. code-block::

      --exclusive --mem=0

GPU NVIDIA MIG (GPU slicing) for the A100 and preemptive jobs will be supported at future dates.

.. _project-job-accounting:

Project and Job Accounting
----------------------------

There are two available commands for tracking usage depending on the project's charging policy.

- For projects that are charged monthly and do not have a specific allocated award amount, such as NGA projects, use the following command to show balance information:

  .. code-block::

     accounts

- For projects that are allocated a fixed amount, such as Illinois Computes projects, use the following command to show balance and deposit info:

  .. code-block::

     accounts-remaining
  
Additional information on job use can be found using the script **jobcharge_grp.py**. The script requires the following arguments:

   .. code-block::

      jobcharge_grp.py [-h] [-detail] accountstring daysback

.. _qos:

.. QOS
.. ----

|
