.. _file-mgmt:

File Management
=================================

.. _small-transfer:

Transferring a Few Small Files
-----------------------------------

These tools are suitable for a few files (typically less than 1,000) and less than 100 GB in total.  If your transfers using these tools take more than **15 minutes**, consider using Globus instead (:ref:`globus`).  

WinSCP [Windows]
~~~~~~~~~~~~~~~~~

If you use a **Windows** machine, you can transfer files between your machine and Hydro using an application called `WinSCP <https://winscp.net/eng/index.php>`_.  

#. Download and install WinSCP.  
#. Open WinSCP and log into the Hydro login node as your **remote** node, using your username, password, and 2FA.  
#. Once you've logged in, WinSCP will work like a drag and drop interface for moving files.  

Secure Copy [Mac and Windows]
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Secure Copy (SCP) is built into all Mac and **most** Windows computers and can be used to securely transfer files between Hydro and other systems. You can find tutorials online for using **scp**. The information you need to use **scp** is:

- The full path name of the file(s) that you want to move.
- The full path name of where you want the file(s) to go.

For example, if the file **my_input_file.dat** is in the **outgoing_data** directory on your local computer. To transfer it to **/u/hirop/input_files** on Hydro:

#. Open a terminal or command prompt.  
#. Change directories to the file location [**outgoing_data**]. 
      
   .. code-block::

      $ cd outgoing_data

#. Verify you are in the correct location, using the ``ls`` command. The file you want to transfer [**my_input_file.dat**] should be listed.
      
   .. code-block::

      $ cd outgoing_data
      $ ls

#. Copy the file to Hydro [**/u/hirop/input_files**] using the following command.
      
   .. code-block::
         
      scp ./my_input_file.dat hirop@hydro.ncsa.illinois.edu:/u/hirop/input_files/

   The output will prompt for your Kerberos password and ask you to initiate a Duo 2FA confirmation. After your authentication is successful, it will transfer the file, printing out progress as it goes.


.. _globus:

Transferring Many Files or Large Files with Globus
---------------------------------------------------

Globus is a web-based file transfer system that works in the background to move files between systems with Globus `endpoints <https://docs.globus.org/faq/globus-connect-endpoints/#what_is_an_endpoint>`_. See `Transferring Files - Globus <https://docs.ncsa.illinois.edu/en/proposed_changes/common/transfer.html#globus>`_ for complete instructions on using Globus.

The Hydro endpoint collection name is: **NFI Hydro**

|
