.. _system-overview:

**System Overview**
==========================

.. _hardware:

Hardware Description
-------------

-  2 Login and 42 Compute nodes
-  Login node (2 ct):

   -  Dell PowerEdge R720
   -  Dual Socket (2) Intel Xeon CPU E5-2690 (8 core, SandyBridge) @ 2.90GHz 20MB
      Cache (16 cores per node) (HT disabled)
   -  384 GB of memory
   
-  Compute node A (33 ct):

   -  Dell PowerEdge R720
   -  Dual Socket (2) Intel Xeon CPU E5-2690 (8 core, SandyBridge) @ 2.90GHz (16 cores per node) (HT disabled)
   -  384 GB of memory
   -  Cache L1/L2/L3: 32/256/20480 KB; L3 Total: 20 MB
   -  NUMA domains: 1 per socket, 2 per node
   -  CPUs per NUMA: domain0={0,2,4,6,8,10,12,14}, domain1={1,3,5,7,9,11,13,15}
   -  40 Gb/s Ethernet
   -  FDR 56Gb/s InfiniBand

-  Compute node B (7 ct):

   -  Dell PowerEdge R7525
   -  Dual Socket (2) AMD EPYC CPU 7452 (32 core, Rome) @ 2.35GHz 
      (64 cores per node) (SMT disabled)
   -  256 GB of memory
   -  Cache L1/L2/L3: 32/512/16384 KB; L3 Total: 128 MB
   -  NUMA domains: 1 per socket, 2 per node
   -  CPUs per NUMA: domain0={0-31}, domain1={32-63}
   -  100 Gb/s Ethernet
   -  FDR 56Gb/s InfiniBand
   -  2 NVIDIA A100 80GB PCIe GPUs

-  Compute node C (2 ct):

   -  Dell PowerEdge R7525
   -  Dual Socket (2) AMD EPYC CPU 7453 (28 core, Milan) @ 2.75GHz
      (56 cores per node) (SMT disabled)
   -  256 GB of memory
   -  Cache L1/L2/L3: 32/512/16384 KB; L3 Total: 64 MB
   -  NUMA domains: 1 per socket, 2 per node
   -  CPUs per NUMA: domain0={0-27}, domain1={28-55}
   -  100 Gb/s Ethernet
   -  FDR 56Gb/s InfiniBand
   -  2 NVIDIA A100 80GB PCIe GPUs

.. _network:

Network
----------

.. _storage:

Storage and File Systems
-------------------------

============  ====================  =========  ============= =========
File System   Path                  OSTs       Default Quota Description
============  ====================  =========  ============= =========
home          /u/<USER>             36          1 TB         Home directory, compiling, source, etc
projects      /projects/<PROJECT>   36          50 TB        Shared project location, datasets, job I/O, etc.
============  ====================  =========  ============= =========

Home Directory Permissions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

By default, user home directories and /projects directories are closed
(permissions 700) with a parent directory setting that prevents users
from opening up the permissions. See the File and Directory Access
Control List page (https://ncsa-hydro-documentation.readthedocs-hosted.com/en/latest/appendices/acl.html) 
page in the Appendix. The /projects file system is designed as
common space for your group; if you want a space that all your group
members can access, that's a good place for it. /projects is also the 
best place for job inputs and outputs.

