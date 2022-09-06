**NCSA Hydro User Documentation**
============================

**1. Introduction**
--------------

The Hydro cluster combines a current OS and software stack, 256 GB of
memory per node, 40 Gb/s WAN bandwidth, and direct high-performance
access to the Blue Waters home, project, and scratch filesystems,
providing several new capabilities for Blue Waters users:

-  Incorporate software that cannot run on the Cray nodes into
   scientific workflows without the need to move data off of Blue
   Waters.
-  Incorporate calculations that require more than 128 GB of memory per
   node into scientific workflows without the need to move data off of
   Blue Waters.
-  Efficiently import/export data to/from external storage services that
   are not supported by Globus Online.

The Hydro cluster is only intended to support workflow components that
require relatively few node hours but cannot run on the Blue Waters Cray
nodes. Due to the small size of the cluster a reasonable effort should
be made to enable the entire workflow in the Cray environment. Access to
the Hydro cluster may be restricted to NGA-related projects with a clear
need for the resource.

**2. Quick Start Guide to Hydro**
---------------------------------

This information is for users who are adept at using BW and are only
interested in the basic workflow.

**1.** `Getting Access <#Access>`__ - Limited to BW Users who need
access to Hydro

**2.** `Log in to Hydro <#Logging%20in>`__ - example: *ssh hydro*

**3.** `Compile Code <#Compiling>`__ - example: *mpicc -o foo.exe foo.c*

**4.** `Run Code <#Run%20Code>`__ - example: *srun -n 1 ./foo.exe*


**5. Level of Expertise Expected for Blue Waters Hydro Users**
--------------------------------------------------------------

Most users of systems like Blue Waters have experience with other large
high-performance computer systems. The instructions on this portal
generally assume that the reader knows how to use a Unix-style command
line, edit files, run (and modify) Makefiles to build code, write
scripts, and submit jobs to a batch queue system. There *are* some
things that work slightly differently on the Cray XE system than other
systems; the portal documentation covers those in detail, but we assume
that you know the basics already.

If you're not at that level yet (if you're unfamiliar with things like
ssh, emacs, vi, jpico, qsub, make, top) then you'll need to gain some
knowledge before you can use Blue Waters effectively. Here are a few
links to resources that will teach you some of the basics about Unix
command line tools and working on a high-performance computing system:

-  https://www.xsede.org/web/xup/online-training
-  https://newton.utk.edu/bin/view/Main/LinuxCommandLineBasics
-  http://websistent.com/linux-acl-tutorial/ # explains linux Access
   Control Lists (ACL) compared with chmod

**Access and Policy**
=====================

Access to the Hydro cluster is limited to users of allocated NFI
projects and is not a generally allocated resource.

If you are part of an allocated NFI project and would like
access to the Hydro cluster please send email to
`help+hydro@ncsa.illinois.edu <mailto:help+delta@ncsa.illinois.edu?subject=access%20to%20Hydro%20cluster>`__
with a justification for your need to use the cluster.


**Logging In**
--------------

Connect to Hydro via the login hosts at
`hydro.ncsa.illinois.edu <http://bw.ncsa.illinois.edu/>`__ using ssh with
your NCSA DUO passcode or push response from your smartphone (see
instructions below)

-  For help activating your NCSA Duo account, reference `this
   page <https://wiki.ncsa.illinois.edu/display/cybersec/Duo+at+NCSA>`__.
-  To check if your NCSA Duo is working properly, visit
   `here <https://duo.security.ncsa.illinois.edu/portal>`__. Depending
   on the choice you make there, you should receive a pass code or a
   push from Duo.

**Open a command prompt (Run command on Windows):**

-  Once on a Blue Waters login node `link to instructions to get on BW
   login
   node <https://wiki.ncsa.illinois.edu/pages/createpage.action?spaceKey=CRAY&title=link+to+instructions+to+get+on+BW+login+node&linkCreation=true&fromPageId=139133071>`__,
   ssh to hydro

   -  ssh hydro


**Frequently Asked Questions**
------------------------------

-  Is my Blue Water's allocation charged for Hydro use?

   -  No. There is currently no plan to charge for use of Hydro. (link
      to How is BW different)

-  I see the following when I log in: Lmod has detected the following
   error: The following module(s) are unknown:...

   -  The modules environments are different between Blue Waters and
      Hydro. `See here. <#BWHomedirs>`__

-  If I have an issue, who do I contact?

   -  help@ncsa.illinois.edu
   -  Mention "Hydro" in the subject line
   
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

