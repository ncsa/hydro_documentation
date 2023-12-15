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

Secure Copy (SCP) is built into all Mac and **most** Windows computers and can be used to securely transfer files between Hydro and other systems. You can find tutorials online for using scp. The information you need to use scp is:

- The full path name of the file(s) that you want to move.
- The full path name of where you want the file(s) to go.

For example, if the file **my_input_file.dat** is located in the **outgoing_data** directory on your local computer. To transfer it to **/u/hirop/input_files** on Hydro:

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

   The output will prompt for your kerberos password and ask you to initiate a Duo 2FA confirmation. After your authentication is successful, it will transfer the file, printing out progress as it goes.


.. _globus:

Transferring Many Files or Large Files With Globus
---------------------------------------------------

Globus is a web-based file transfer system that works in the background to move files between systems with **Globus Collections**. Hydro's Globus endpoint is called **NFI Hydro**. To transfer files to and from your directories using Globus, you will have to authenticate that endpoint, using your NCSA username, password, and NCSA Duo 2FA. 

One-time Setup
~~~~~~~~~~~~~~~~

You will need to set up a separate account on globus.org, that will have a username and a separate password. To use Globus to transfer files to and from Hydro, you will need to *link* your new Globus account with your NCSA identity. 

#. Log into `globus.org <https://globus.org>`_. 
#. Click on **Settings** in the left sidebar.
#. Click on the **Account** tab. If your NCSA username and email address is not in that list, then click **Link Another Identity** in the upper right to link it.

Using Globus to Transfer Files
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

After your NCSA identity is linked in Globus, do the following to transfer files.

#. Navigate to `globus.org <https://globus.org>`_.
#. Click **Log In** in the upper right corner.
#. Choose **National Center for Supercomputing Applications** as your Identity Provider and click **Continue**.

   .. image:: images/file-mgmt/globus-organizational-login.png
      :alt: Globus organizational login screen.

#. If prompted, click **Allow** when asked to authorized the Globus Web App.

   .. image:: images/file-mgmt/globus-info-services-allow.png
      :alt: Globus web app information and services allow screen.

#. Login in via the Illinois Shibboleth service, this will be a Duo 2FA prompt.

#. Once in the **File Manager** section, click on **collection**.  
#. Search for **NFI Hydro** and click on the **NFI Hydro** collection.

   .. image:: images/file-mgmt/globus-nfi-hydro.png
      :alt: Globus file amanger "NFI Hydro" collection search.

#. The system will prompt you to Authenticate to the endpoint, click **continue**. 
#. If prompted, link your \netid@illinois.edu identity.

   .. image:: images/file-mgmt/globus-authentication-consent.png
      :alt: Globus authenitcation/consent for Globus to manage data on the collection screen.

   .. image:: images/file-mgmt/globus-identity-required.png
      :alt: Globus identity required screen.

   .. image:: images/file-mgmt/globus-illinois-research-storage-info-services-allow.png
      :alt: Globus Illinois Research Storage web app informatoin and services allow screen.

   You should then get dropped back into the “File Manger” view and be able to see your home directory in the explorer window.

   .. image:: images/file-mgmt/hydro-globus-file-manager.png
      :alt: Globus file manager NFI Hydro screen.

#. In a similar manner (in the right half of the **File Manger** view), search for and authenticate to the collection you are planning to transfer data to/from.
#. Use the GUI to transfer the data; you can choose transfer settings. Also on the left is a button to view your current transfer activity.

   .. image:: images/file-mgmt/globus-activity-transfer.png
      :alt: Globus activity transfer screen.

|
