.. _partitions-job-policies:

Partitions and Job Policies
===========================

This page lists job partitions, job limits, and QOS considerations for submitting
jobs to the Hydro cluster.


**Partitions (Queues)**
-----------------------

Table.Hydro Partitions/Queues

+---------------+---------------+----------+----------+----------+----------+
| **Partition   | **Node        | **Max    | **Max    | **Max    | **Charge |
|  /Queue**     | Type**        | Nodes    | Du       | Running  | Factor** |
|               |               | per      | ration** | in       |          |
|               |               | Job**    |          | Queue/   |          |
|               |               |          |          | user\*** |          |
+---------------+---------------+----------+----------+----------+----------+
| cpu           | CPU           | TBD      | 24 hr /  | 8,448    | 1.0      |
|               |               |          | 48 hr    | cores    |          |
+---------------+---------------+----------+----------+----------+----------+
| cpu-int       | CPU           | TBD      | 30 min   | in total | 2.0      |
| eractive      |               |          |          |          |          |
+---------------+---------------+----------+----------+----------+----------+
| gpuA100x4     | quad          | TBD      | 24 hr /  | 3,200    | 1.0      |
|               | A100          |          | 48 hr    | cores    |          |
|               |               |          |          | and 200  |          |
|               |               |          |          | gpus     |          |
+---------------+---------------+----------+----------+----------+----------+
| gpuA100x4     | quad-A100     | TBD      | 30 min   | in total | 2.0      |
| -interactive  |               |          |          |          |          |
|               |               |          |          |          |          |
+---------------+---------------+----------+----------+----------+----------+
| gpuA100x8     | octa-A100     | TBD      | 24 hr /  | TBD      | 2.0      |
|               |               |          | 48 hr    |          |          |
+---------------+---------------+----------+----------+----------+----------+
| gpuA100x8     | octa-A100     | TBD      | 30 min   | TBD      | 4.0      |
| -interactive  |               |          |          |          |          |
|               |               |          |          |          |          |
+---------------+---------------+----------+----------+----------+----------+
| gpuA40x4      | quad-A40      | TBD      | 24 hr /  | 3,200    | 0.6      |
|               |               |          | 48 hr    | cores    |          |
|               |               |          |          | and 200  |          |
|               |               |          |          | gpus     |          |
+---------------+---------------+----------+----------+----------+----------+
| gpuA40x4      | quad-A40      | TBD      | 30 min   | in total | 1.2      |
| -interactive  |               |          |          |          |          |
|               |               |          |          |          |          |
+---------------+---------------+----------+----------+----------+----------+
| gpuMI100x8    | octa-MI100    | TBD      | 24 hr /  | TBD      | 1.5      |
|               |               |          | 48 hr    |          |          |
+---------------+---------------+----------+----------+----------+----------+
| gpuMI100x8    | octa-MI100    | TBD      | 30 min   | TBD      | 3.0      |
| -interactive  |               |          |          |          |          |
|               |               |          |          |          |          |
+---------------+---------------+----------+----------+----------+----------+

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
