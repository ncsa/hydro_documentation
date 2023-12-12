.. meta::
    :google-site-verification: D6d2MOvDRon7baT8kQbEmeq6Uvmnrgy7lxwNffyIujw

##########################
Hydro User Documentation
#########################

Introduction
======================

The Hydro cluster combines a current OS and software stack, up to 512 GB of
memory per node, up to 100 Gb/s WAN bandwidth, and direct access to two Lustre-based parallel filesystems (/home and /projects):

.. _expected-experience:

Level of Expertise Expected for Hydro Users
===============================================

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

===================

.. toctree::
   :maxdepth: 2
   :hidden:

   status-updates
   quick-start
   faq
   support-services
   help

.. toctree::
   :maxdepth: 2
   :caption: User Guide
   
   user-guide/system_description
   user-guide/illinois_computes
   user-guide/accessing
   user-guide/file-mgmt
   user-guide/prog-env
   user-guide/containers
   user-guide/partitions-policies
   user-guide/running-jobs
   user-guide/acl
