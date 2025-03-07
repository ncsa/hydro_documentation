.. _architecture:

System Architecture
====================

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

Dell PowerEdge R720 Compute Node Specifications [2.0GHz]
$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$

-  Number of nodes: 27
-  Dual Socket (2) Intel Xeon CPU E5-2690 (8 core, SandyBridge) @ **2.0GHz** (16 cores per node) (HT disabled)
-  384 GB of memory
-  Cache L1/L2/L3: 32/256/20480 KB; L3 Total: 20 MB
-  NUMA domains: 1 per socket, 2 per node
-  CPUs per NUMA: domain0={0,2,4,6,8,10,12,14}, domain1={1,3,5,7,9,11,13,15}
-  40 Gb/s Ethernet

Dell PowerEdge R815 Compute Node Specifications
$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$

-  Number of nodes: 4
-  Quad Socket (4)  (16 core, AMD Interlagos) @ 2.30GHz (64 cores per node)
-  512 GB of memory
-  Cache L1/L2/L3: .768/16/16 MB; L3 Total: 32 MB
-  NUMA domains: 2 per socket, 8 per node
-  CPUs per NUMA: domain0={0-7} domain1={8-15} domain2={32-39} domain3={40-47} domain4={48-55} domain5={56-63} domain6={16-23} domain7={24-31}
-  40 Gb/s Ethernet

Dell PowerEdge R7525 Compute Node Specifications
$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$

-  Number of nodes: 7
-  Dual Socket (2) AMD EPYC CPU 7452 (32 core, Rome) @ 2.35GHz (64 cores per node) (SMT disabled)
-  256 GB of memory
-  Cache L1/L2/L3: 32/512/16384 KB; L3 Total: 128 MB
-  NUMA domains: 1 per socket, 2 per node
-  CPUs per NUMA: domain0={0-31}, domain1={32-63}
-  100 Gb/s Ethernet
-  1.5 TB NVME (/tmp)
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
-  1.5 TB NVME (/tmp)
-  2 NVIDIA A100 80GB PCIe GPUs


.. _network:

.. Network
.. ----------

.. _storage:

Storage and File Systems
-------------------------

.. table:: Hydro Storage and File Systems

   +------------------------------+-----------------+-----------+---------------------+----------------------------+
   | File System                  | Media Type      | Total Size| Default Quota       | Backups                    |                 
   +==============================+=================+===========+=====================+============================+
   | Home (/u)                    | NVME            | n/a       | 100 GB, 500k files  | None                       |   
   +------------------------------+-----------------+-----------+---------------------+----------------------------+
   | Projects (/projects)         | HDD, NVME cache | n/a       | 50 TB, 750k files   | None                       | 
   +------------------------------+-----------------+-----------+---------------------+----------------------------+
   | Temp (/tmp) - GPU nodes only | Local NVME      | 1.5TB     | n/a                 | Cleared after each job     |                 
   +------------------------------+-----------------+-----------+---------------------+----------------------------+
   | Taiga (/taiga)               | HDD, NVME cache | >19PB     | `Must be purchased`_| `See Taiga documentation`_ |                 
   +------------------------------+-----------------+-----------+---------------------+----------------------------+

.. _must be purchased: https://docs.ncsa.illinois.edu/systems/taiga/

.. _See Taiga documentation: https://docs.ncsa.illinois.edu/systems/taiga/en/latest/user-guide/data-recovery.html

Home
~~~~~~~~

The home (**/u**) area of the file system is where users land upon logging into the cluster via SSH. Home is NFS based, lower space than projects but highly responsive. Example uses for home are scripts, source code, and compiling.

Home Directory Permissions
$$$$$$$$$$$$$$$$$$$$$$$$$$$$$

By default, user home directories and /projects directories are closed (permissions 700) with a parent directory setting that prevents users from opening the permissions (see :ref:`acl`). 

Projects
~~~~~~~~~~

The projects (**/projects**) area is where a group's storage capacity resides. Projects is Lustre mount type with progressive layout file striping. The projects file system is designed as common space for your group. Projects is also the best place for job input and output.

Temp
~~~~~~~~~~

The local temp space is intended for per-node scratch use during a job, and it is cleared between jobs. It can be accessed simply by using /tmp.  Local NVME temp space is only a feature on GPU nodes. On all others, /tmp will reside in host memory.

Taiga
~~~~~~~~~~~~~~~~~~~~

If a Taiga allocation has been purchased, it can be accessed on any hydro node under (**/taiga**) . It is a Lustre mount type with progressive layout file striping. Taiga can be used to share data across NCSA resources.

|
