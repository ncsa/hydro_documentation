**********************************
**Hydro User Documentation**
**********************************

.. warning::

   This documentation is currently (fall 2022) being ported to readthedocs.com.  Information here is believe to be valid, but might be slightly       incomplete as we fill in the rest of the pages.  

**Introduction**
======================

The Hydro cluster combines a current OS and software stack, up to 384 GB of
memory per node, 40 Gb/s WAN bandwidth, and direct access to two Lustre-based parallel filesystems (/home and /projects):


.. _quick-start:

**Quick Start Guide to Hydro**
-------------------------------

This information is for users who are adept at using an HPC system and are only
interested in the basic Hydro workflow.

**1.** :ref:`access-and-policy` - Limited to NFI projects and Illinois Computes projects that need
access to the Hydro compute resource.

**2.** :ref:`logging-in` - example: *ssh hydro.ncsa.illinois.edu*

**3.** :ref:`compiling` - example: *mpicc -o foo.exe foo.c*

**4.** :ref:`running` - example: *srun -n 1 ./foo.exe*

**5.** :ref:`partitions-job-policies` - Job Policies documentation

**6.** :ref:`slurm` - Slurm job control software

**7.** :ref:`sample-batch-script` - Sample batch script

.. _expected-experience:

Level of Expertise Expected for Hydro Users
--------------------------------------------------------------

The instructions on this portal
generally assume that the reader knows how to use a Unix-style command
line, edit files, run (and modify) Makefiles to build code, write
scripts, and submit jobs to a batch queue system.

If you're not at that level yet (if you're unfamiliar with things like
ssh, emacs, vi, jpico, srun, make, top) then you'll need to gain some
knowledge before you can use Hydro effectively. Here are a few
links to resources that will teach you some of the basics about Unix
command-line tools and working on a high-performance computing system:

-  https://portal.tacc.utexas.edu/-/linux-unix-basics-for-hpc
-  http://websistent.com/linux-acl-tutorial/ # explains linux Access
   Control Lists (ACL) compared with chmod

.. _access-and-policy:

Access and Policy
----------------------

Access to the Hydro cluster is limited to users of allocated NFI
projects and Illinois Computes projects. Please see https://wiki.ncsa.illinois.edu/display/FIN/Hydro 
for additional information on non-NFI funded access to the Hydro cluster.

If you are part of an allocated NFI project and would like
access to the Hydro cluster please send email to
`help+hydro@ncsa.illinois.edu <mailto:help+delta@ncsa.illinois.edu?subject=access%20to%20Hydro%20cluster>`__
with a justification for your need to use the cluster.

.. _logging-in:

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


**Account Management**
----------------------
 
To manage a Hydro project group: add and remove users or set a group 
delegate, please see the NCSA Allocation and Account Management page at 
https://wiki.ncsa.illinois.edu/display/USSPPRT/NCSA+Allocation+and+Account+Management
.

.. _faq:

Frequently Asked Questions
------------------------------

How do I get help if I can't find the answer in the documentation?  
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
If you can't find the answer in the documentation (or via the search bar in the upper left corner) please submit a ticket (next topic).  The ticket becomes a discussion of your problem and the path to a solution.  

..  _submit-ticket:

How do I submit a ticket about Hydro?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
To open a help ticket, send an email to: help+hydro@ncsa.illinois.edu.  Be sure "HYDRO" is in the subject line and put as much information and background about your problem or question in the body of the message.  You should receive a return email with a reference to the ticket within one business day.  
   
   
Hydro Documentation Table of Contents
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   
.. toctree::
   :maxdepth: 2
   
   index
   quick_start_guide
   system_description
   accessing_transferring_files
   programming_environments
   containers
   partitions_and_job_policies
   running
   support_and_services
   tools_and_utilities
   appendices/index
