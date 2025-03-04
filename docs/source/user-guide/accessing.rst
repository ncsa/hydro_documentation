.. _accessing:

Hydro Login Methods
==================
.. Note::
    All users must have a valid NCSA account with DUO setup in order to access the Hydro 
    system. For help with your account or getting an allocation on Hydro, please see the :ref:`accounts` page.

Once you have an approved Hydro allocation, the primary methods for accessing Hydro are:
   
    - :ref:`connecting_ssh` - Most common login method for users.
    - :ref:`vs_code_ssh` - Visual Studio Code extension that allows you to connect to Hydro through VS Code

.. _connecting_ssh:

Connecting with SSH
----------------------

Direct access to Hydro is available via SSH. 

To connect to Hydro via SSH, use the following command where `<username>` is replaced by your NCSA 
account username:

.. code-block:: terminal

    ssh <username>@hydro.ncsa.illinois.edu

**Authentication and DUO MFA**

Upon connecting, you will be prompted to enter your NCSA password.

.. code-block:: terminal

    <username>@hydro.ncsa.illinois.edu's password:

After successfully entering your password, you'll be prompted to authenticate with a two-factor 
method with a message like this:

.. code-block:: terminal

    (<username>@hydro.ncsa.illinois.edu) Duo two-factor login for <username>
    Enter a passcode or select one of the following options:

    1. Duo Push to XXX-XXX-1234
    2. Phone call to XXX-XXX-1234
    3. SMS passcodes to XXX-XXX-1234

    Passcode or option (1-3):


NCSA requires multifactor authentication (MFA) for all users. You can choose one of the options 
listed to authenticate. Once your MFA method is accepted, you will be connected to one of Hydro's 
login nodes.

.. Note::
    **Login node usage policy**
    
    Login nodes are shared among all users and are intended for file management, job submission, 
    and other tasks that do not require significant computational resources. Please do not run 
    computationally intensive jobs on the login nodes. Please see the :ref:`running` page 
    for information on submitting jobs to the compute nodes.

.. _vs_code_ssh:

VS Code Remote SSH extension
-------------------------------

The Visual Studio Code Remote - SSH extension allows you to connect your VS Code window to a remote 
system via SSH and take full advantage of VS Code's feature set. You can find the extension 
through VS Code's built in extension browser or by visiting the 
`VS Code Marketplace <https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh>`_.

#. Install the Remote - SSH extension into VS Code

    ..  figure:: images/accessing/01_remote_ssh.png
        :alt: Remote ssh extension in VS Code.
        :figwidth: 550px
        :width: 500px

#. Follow the `VS Code connect to a remote host <https://code.visualstudio.com/docs/remote/ssh#_connect-to-a-remote-host>`_ instructions. 

#. Once connected to Hydro, you can interact with the remote system just like you would with your local machine.
