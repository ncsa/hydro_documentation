.. meta::
    :google-site-verification: D6d2MOvDRon7baT8kQbEmeq6Uvmnrgy7lxwNffyIujw

**********************************
**Hydro User Documentation**
**********************************

**Introduction**
======================

The Hydro cluster combines a current OS and software stack, up to 512 GB of
memory per node, up to 100 Gb/s WAN bandwidth, and direct access to two Lustre-based parallel filesystems (/home and /projects):

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

.. _faq:

Frequently Asked Questions
------------------------------

How do I get help if I can't find the answer in the documentation?  
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
If you can't find the answer in the documentation (or via the search bar in the upper left corner) please submit a ticket (next topic).  The ticket becomes a discussion of your problem and the path to a solution.  

..  _submit-ticket:

How do I submit a ticket about Hydro?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Email help+hydro@ncsa.illinois.edu with the following:

- A descriptive subject line starting with "HYDRO:" (e.g., "HYDRO: Permission denied error loading blorg module")
- What you are actually trying to accomplish (e.g., run multi-blorg regression analysis on 2.4 million files)
- Commands or scripts you ran (in enough detail to reproduce the problem)
- Complete error and other messages as text (not screenshots)
- The list of loaded modules from running "module list"
- If your command or script worked in the past (and when it stopped working)
- Any other machines where the problem does not occur (e.g., Delta or campus cluster)
- Any other approaches you have tried
- Any other information you think might be relevant

You should receive a reply with a reference to the ticket within one business day.  
   
   
Hydro Documentation Table of Contents
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   
.. toctree::
   :maxdepth: 2
   
   index
   quick_start_guide
   system_description
   illinois_computes
   accessing_transferring_files
   programming_environments
   containers
   partitions_and_job_policies
   running
   support_and_services
   tools_and_utilities
   appendices/index
