**System Description**
==========================

Hardware
-------------

-  2 Login and 42 Compute nodes
-  Compute node A (33 ct):

   -  Dell PowerEdge R720
   -  Dual Socket (2) Intel Xeon CPU E5-2690 (8 core) @ 2.90GHz 20MB
      Cache (16 cores per node) (HT disabled)
   -  384 GB of memory
   -  40 Gb/s Ethernet
   -  FDR 56Gb/s InfiniBand

-  Compute node B (7 ct):

   -  Dell PowerEdge R7525
   -  Dual Socket (2) AMD EPYC CPU 7452 (32 core) @ 2.35GHz 128MB Cache
      (64 cores per node) (SMT disabled)
   -  256 GB of RAM
   -  100 Gb/s Ethernet
   -  FDR 56Gb/s InfiniBand
   -  2 NVIDIA A100 80GB PCIe GPUs

-  Compute node C (2 ct):

   -  Dell PowerEdge R7525
   -  Dual Socket (2) AMD EPYC CPU 7453 (28 core) @ 2.75GHz 64MB Cache
      (56 cores per node) (SMT disabled)
   -  256 GB of memory
   -  100 Gb/s Ethernet
   -  FDR 56Gb/s InfiniBand
   -  2 NVIDIA A100 80GB PCIe GPUs

Storage and File Systems
-------------------------

============  ====================  =========  ============= =========
File System   Path                  OSTs       Default Quota Description
============  ====================  =========  ============= =========
home          /u/<USER>             36          1 TB         Home directory, compiling, source, etc
projects      /projects/<PROJECT>   36          50 TB        Shared project location, datasets, job I/O, etc.
============  ====================  =========  ============= =========
