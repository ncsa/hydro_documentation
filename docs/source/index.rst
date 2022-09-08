**********************************
**NCSA Hydro User Documentation**
**********************************

**Introduction**
======================

The Hydro cluster combines a current OS and software stack, 384 GB of
memory per node, 40 Gb/s WAN bandwidth, and direct access to two Lustre-based parallel filesystems (/home and /projects):


**Quick Start Guide to Hydro**
-------------------------------

This information is for users who are adept at using BW and are only
interested in the basic workflow.

**1.** `Getting Access <#Access>`__ - Limited to BW Users who need
access to Hydro

**2.** `Log in to Hydro <#Logging%20in>`__ - example: *ssh hydro*

**3.** `Compile Code <#Compiling>`__ - example: *mpicc -o foo.exe foo.c*

**4.** `Run Code <#Run%20Code>`__ - example: *srun -n 1 ./foo.exe*


Level of Expertise Expected for Blue Waters Hydro Users
--------------------------------------------------------------

The instructions on this portal
generally assume that the reader knows how to use a Unix-style command
line, edit files, run (and modify) Makefiles to build code, write
scripts, and submit jobs to a batch queue system.

If you're not at that level yet (if you're unfamiliar with things like
ssh, emacs, vi, jpico, srun, make, top) then you'll need to gain some
knowledge before you can use Blue Waters effectively. Here are a few
links to resources that will teach you some of the basics about Unix
command line tools and working on a high-performance computing system:

-  https://www.xsede.org/web/xup/online-training
-  https://newton.utk.edu/bin/view/Main/LinuxCommandLineBasics
-  http://websistent.com/linux-acl-tutorial/ # explains linux Access
   Control Lists (ACL) compared with chmod

Access and Policy
----------------------

Access to the Hydro cluster is limited to users of allocated NFI
projects.

If you are part of an allocated NFI project and would like
access to the Hydro cluster please send email to
`help+hydro@ncsa.illinois.edu <mailto:help+delta@ncsa.illinois.edu?subject=access%20to%20Hydro%20cluster>`__
with a justification for your need to use the cluster.


**Logging In**
--------------

Connect to Hydro via the login hosts at
hydro.ncsa.illinois.edu using ssh with
your NCSA DUO passcode or push response from your smartphone (see
instructions below)

-  For help activating your NCSA Duo account, reference `this
   page <https://wiki.ncsa.illinois.edu/display/cybersec/Duo+at+NCSA>`__.
-  To check if your NCSA Duo is working properly, visit
   `here <https://duo.security.ncsa.illinois.edu/portal>`__. Depending
   on the choice you make there, you should receive a pass code or a
   push from Duo.


**Frequently Asked Questions**
------------------------------

-  If I have an issue, who do I contact?

   -  help+hydro@ncsa.illinois.edu
   
   
Hydro Documentation Table of Contents
------------------------------
   
.. toctree::
   :maxdepth: 2
   
   quick_start_guide
   system_description
   accessing_transferring_files
   programming_environments
   partitions_and_job_policies
   running
   support_and_services
   tools_and_utilities

