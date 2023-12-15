.. _system-overview:

System Overview
==================

.. _hardware:

Hardware Description
---------------------

Hydro includes 2 login nodes and 68 compute nodes.

Login Nodes
~~~~~~~~~~~~~

-  Number of nodes: 2
-  Dell PowerEdge R720
-  Dual Socket (2) Intel Xeon CPU E5-2690 (8 core, SandyBridge) @ 2.90GHz 20MB Cache (16 cores per node) (HT disabled)
-  384 GB of memory

Compute Nodes
~~~~~~~~~~~~~~~

Dell PowerEdge R720 Compute Node Specifications [2.90GHz]
$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$

-  Number of nodes: 28
-  Dual Socket (2) Intel Xeon CPU E5-2690 (8 core, SandyBridge) @ **2.90GHz** (16 cores per node) (HT disabled)
-  384 GB of memory
-  Cache L1/L2/L3: 32/256/20480 KB; L3 Total: 20 MB
-  NUMA domains: 1 per socket, 2 per node
-  CPUs per NUMA: domain0={0,2,4,6,8,10,12,14}, domain1={1,3,5,7,9,11,13,15}
-  40 Gb/s Ethernet
-  FDR 56Gb/s InfiniBand

Dell PowerEdge R720 Compute Node Specifications [2.0GHz]
$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$

-  Number of nodes: 27
-  Dual Socket (2) Intel Xeon CPU E5-2690 (8 core, SandyBridge) @ **2.0GHz** (16 cores per node) (HT disabled)
-  384 GB of memory
-  Cache L1/L2/L3: 32/256/20480 KB; L3 Total: 20 MB
-  NUMA domains: 1 per socket, 2 per node
-  CPUs per NUMA: domain0={0,2,4,6,8,10,12,14}, domain1={1,3,5,7,9,11,13,15}
-  40 Gb/s Ethernet
-  FDR 56Gb/s InfiniBand

Dell PowerEdge R815 Compute Node Specifications
$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$

-  Number of nodes: 4
-  Quad Socket (4)  (16 core, AMD Interlagos) @ 2.30GHz (64 cores per node)
-  512 GB of memory
-  Cache L1/L2/L3: .768/16/16 MB; L3 Total: 32 MB
-  NUMA domains: 2 per socket, 8 per node
-  CPUs per NUMA: domain0={0-7} domain1={8-15} domain2={32-39} domain3={40-47} domain4={48-55} domain5={56-63} domain6={16-23} domain7={24-31}
-  40 Gb/s Ethernet
-  QDR 40 Gb/s InfiniBand

Dell PowerEdge R7525 Compute Node Specifications
$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$

-  Number of nodes: 7
-  Dual Socket (2) AMD EPYC CPU 7452 (32 core, Rome) @ 2.35GHz (64 cores per node) (SMT disabled)
-  256 GB of memory
-  Cache L1/L2/L3: 32/512/16384 KB; L3 Total: 128 MB
-  NUMA domains: 1 per socket, 2 per node
-  CPUs per NUMA: domain0={0-31}, domain1={32-63}
-  100 Gb/s Ethernet
-  FDR 56Gb/s InfiniBand
-  2 NVIDIA A100 80GB PCIe GPUs

Dell PowerEdge R7525 Compute Node Specifications
$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$

-  Number of nodes: 2
-  Dual Socket (2) AMD EPYC CPU 7453 (28 core, Milan) @ 2.75GHz (56 cores per node) (SMT disabled)
-  256 GB of memory
-  Cache L1/L2/L3: 32/512/16384 KB; L3 Total: 64 MB
-  NUMA domains: 1 per socket, 2 per node
-  CPUs per NUMA: domain0={0-27}, domain1={28-55}
-  100 Gb/s Ethernet
-  FDR 56Gb/s InfiniBand
-  2 NVIDIA A100 80GB PCIe GPUs


.. _network:

.. Network
.. ----------

.. _storage:

Storage and File Systems
-------------------------

.. list-table::
   :stub-columns: 1

   * - File System
     - Home
     - Projects
     - Taiga (coming soon)
   * - Path
     - /u/<USER>
     - /projects/<PROJECT>
     - /taiga/...
   * - Media Type
     - HDD
     - HDD
     - HDD, NVME cache
   * - Mount Type
     - Lustre
     - Lustre
     - Lustre
   * - File Striping
     - Fixed Size
     - Fixed Size
     - Progressive Layout
   * - Total Size
     - 2 PB
     - 2 PB
     - >19 PB
   * - Default Quota
     - 1 TB, 6M files
     - 50 TB, 1M files
     - `Must be purchased <https://wiki.ncsa.illinois.edu/display/TG/>`_
   * - Backups
     - None
     - None
     - `Snapshots <https://wiki.ncsa.illinois.edu/display/TG/Taiga+User+Guide#TaigaUserGuide-DataRecovery)>`_
   * - Example Uses
     - Scripts, source code, compiling
     - Shared data, job I/O
     - Sharing data across NCSA resources

.. table:: Hydro Storage and File Systems

   +---------------+-----------------+------------+-------------------+-------+---------------------+-------------+-----------------------+
   | File System   | Media Type      | Mount Type | File Striping     | Total | Default Quota       | Backups     | Example Uses          |
   |               |                 |            |                   |       |                     |             |                       |
   |               |                 |            |                   | Size  |                     |             |                       |
   +===============+=================+============+===================+=======+=====================+=============+=======================+
   | Home (/u/)    | HDD             | Lustre     | Fixed Size        | 2PB   | 1 TB, 6M files      | None        | Scripts, source code, |
   |               |                 |            |                   |       |                     |             |                       |
   |               |                 |            |                   |       |                     |             | compiling             |
   +---------------+-----------------+------------+-------------------+-------+---------------------+-------------+-----------------------+
   | Projects      | HDD             | Lustere    | Fixed Size        | 2PB   | 50 TB, 1M files     | None        | Shared data, job I/O  |
   |               |                 |            |                   |       |                     |             |                       |
   | (/projects/)  |                 |            |                   |       |                     |             |                       |
   +---------------+-----------------+------------+-------------------+-------+---------------------+-------------+-----------------------+
   | *coming soon* | HDD, NVME cache | Lustre     | Progressive Layout| >19PB | `must be purchased`_| `snapshots`_| Sharing data across   |
   |               |                 |            |                   |       |                     |             |                       |
   | Taiga         |                 |            |                   |       |                     |             | NCSA resources        |
   |               |                 |            |                   |       |                     |             |                       |
   | (/taiga/)     |                 |            |                   |       |                     |             |                       |
   +---------------+-----------------+------------+-------------------+-------+---------------------+-------------+-----------------------+

.. _must be purchased: https://wiki.ncsa.illinois.edu/display/TG/

.. _snapshots: https://wiki.ncsa.illinois.edu/display/TG/Taiga+User+Guide#TaigaUserGuide-DataRecovery)

Home Directory Permissions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

By default, user home directories and /projects directories are closed (permissions 700) with a parent directory setting that prevents users from opening up the permissions (see :ref:`acl`). 
The /projects file system is designed as common space for your group. /projects is also the best place for job input and output.

