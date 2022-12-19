.. _partitions-job-policies:

Partitions and Job Policies
===========================

This page lists job partitions, job limits, and QOS considerations for submitting
jobs to the Hydro cluster.


**Partitions (Queues)**
-----------------------

Table.Hydro Partitions/Queues

+---------------+---------------+----------+---------------+----------+----------+
| **Partition   | **Node/Job    | **Max    | **Max**       | **Max    | **Charge |
| Queue**       | Type**        | Nodes    | **Duration**  | Running  | Factor** |
|               |               | per      |               | in       |          |
|               |               | Job**    |               | Queue/   |          |
|               |               |          |               | user\*** |          |
+---------------+---------------+----------+---------------+----------+----------+
| sandybridge   | CPU           | TBD      | 7 days        | TBD      | 1.0      |
+---------------+---------------+----------+---------------+----------+----------+
| milan         | CPU           | TBD      | 7 days        | TBD      | TBD      |
+---------------+---------------+----------+---------------+----------+----------+
| rome          | CPU           | TBD      | 7 days        | TBD      | TBD      |
+---------------+---------------+----------+---------------+----------+----------+
| a100          | dual A100 GPU | TBD      | 7 days        | TBD      | TBD      |
|               | w/ any CPU    |          |               |          |          |
+---------------+---------------+----------+---------------+----------+----------+
| a100milan     | dual A100 GPU | TBD      | 7 days        | TBD      | TBD      |
|               | w/ Milan CPU  |          |               |          |          |
+---------------+---------------+----------+---------------+----------+----------+
| a100rome      | dual A100 GPU | TBD      | 7 days        | TBD      | TBD      |
|               | w/ Rome CPU   |          |               |          |          |
+---------------+---------------+----------+---------------+----------+----------+

sview view of slurm partitions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Node Policies
~~~~~~~~~~~~~

Node-sharing is the default for jobs. Node-exclusive mode can be
obtained by specifying all the consumable resources for that node type
or adding the following Slurm options:

::

   --exclusive --mem=0

GPU NVIDIA MIG (GPU slicing) for the A100 will be supported at a future
date.

Pre-emptive jobs will be supported at a future date.

.. _qos:

QOS
----
