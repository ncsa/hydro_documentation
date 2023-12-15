.. _acl:

File and Directory Access Control List (ACL)
============================================

Default ownership and permissions are modified to address the issue of unintentional overly broad grants of directory permissions.

Filesystem ACL change restriction defaults:

-  Default ACL for new file creation is 600 instead of 644 (**default umask changing from 022 to 077**).
-  All **top level folders will not permit ACL changes by users** (home, projects).
-  Though ACL expansion of subfolders isn't permitted by default, a **service request can be made to enable either ACL self management or a specific ACL change enabled by administrators**.

Recommended practice:

-  Use projects directory to share within project account members.
-  Expand access only to *what* you intend to *whom* you intend. chmod is allowed, but setfacl is preferred.
-  Periodically review your file and folder permissions (getfacl shows all extended attributes).

.. _acl-home-dir:

Home Directories
----------------

Default home directories will have the following setting shown below.
Note that root is both owner and group, and the '+' indicates additional attributes are present; in the example below, extended attributes for ACLs are enabled. 
Full ACL listing can be queried with the getfacl command as shown. 
Note: *The Posix representation of the top level directory ACL represents a "calculated effective mask" of 770 (drwxrwx\--\-+), because additional extended attributes grant rwx to another user, in this case, "username". 
This can be interpreted exactly like a mask of 700 for user username.*

.. code-block:: 

   hydrol1:~> ls -ld ~                                             
   drwxrwx---+ 113 root root 53248 Dec 18 13:39 /u/username         

   hydrol1:~> getfacl ~                                            
   getfacl: Removing leading '/' from absolute path names           
   # file: u/username                                             
   # owner: root                                                   
   # group: root                                                    
   user::rwx                                                       
   user:username:rwx                                               
   group::---                                                      
   mask::rwx                                                         
   other::---                                                      


.. _acl_project_dir:

Project Directory
-----------------

Project directories will have similar restrictions as home, with the exception that files here will be group accessible (will override umask). 
The respective project group will own files created in the project directory by default, overriding the user primary group if it differs.

.. _enabling_acl:

Enabling ACL Modification (if needed)
-------------------------------------

Enabling access to others in the same group
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Use your project space (/projects/psn) if you are sharing with others in your same project. 
This is what the space is designed for. 
Please submit a service request with any exceptions to be evaluated.

Enabling access to others outside of a group
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To enable access to directories and files residing within your home directory you need to:

#. Submit a ticket asking for an "ACL change request" with the top level folder you wish to be traverseable, and by whom. e.g. I would like my group "X" to be able to have read and write access to a subdirectory of my home directory. 

#. Depending on the request, an admin will either:

   -  Set a specific ACL grant as requested
   -  Set the top level to an effective 701 permission, (drwx\--\--\-x ). This will allow traversal into your top-level directory by anyone on the system to access any file or folder according to its own specific permission limitations.

#. An admin will check for any custom umask setting in your local environment setup that may result in unintentional data exposure in combination with requested ACL changes.

#. If self-managed, begin modifying ACLs on desired subfolders using chmod or setfacl. setfacl is strongly preferred due to its ability to be much more specific with user/group/mask combinations. Support staff can provide any additional best practice guidance requested to help you configure ACL layouts that serve your objective.

To enable access for a specific user from another group to a file or directory
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Below is an example where user1 adds read access to a file for user2 using setfacl and then checking the permissions using getfacl. 
Note that the permissions for the parent directory need to allow for "o+x" as mentioned above.

.. code-block:: 

   user1@hydrol1:~> touch abc                                        
   user1@hydrol1:~> ls -l abc                                        
   -rw------- 1 user1 hydro_bbmb 0 Dec 19 08:45 abc                  
   user1@hydrol1:~> setfacl -m "u:user2:r" abc                       
   user1@hydrol1:~> ls -l abc                                        
   -rw-r-----+ 1 user1 hydro_bbmb 0 Dec 19 08:45 abc                 
   user1@hydrol1:~> getfacl abc                                      
   # file: abc                                                       
   # owner: user1                                                    
   # group: hydro_bbmb                                               
   user::rw-                                                          
   user:user2:r--                                                    
   group::---                                                        
   mask::rwx                                                         
   other::---                                                        

Below is an example where user1 adds read+execute access to a directory for user2 using setfacl and then checking the permissions using getfacl. 
Note that the permissions for the parent directory need to allow for "o+x" as mentioned above.

.. code-block::

   user1@hydrol1:~> mkdir abc                                         
   user1@hydrol1:~> getfacl abc                                        
   # file: abc                                                         
   # owner: user1                                                      
   # group: hydro_bbmb                                                 
   user::rwx group::--- other::---                                     
   user1@hydrol1:~> setfacl -m "u:user2:rx" abc                        
   user1@hydrol1:~> getfacl abc                                        
   # file: abc                                                         
   # owner: user1                                                    
   # group: hydro_bbmb                                                
   user::rwx                                                          
   user:user2:r-x                                                 
   group::---                                                      
   mask::r-x                                                       
   other::---                                                       
   user1@hydrol1:~>ls -ld abc                                       
   drwxr-x---+ 2 gbauer hydro_bbmb 4096 Dec 19 09:13 abc             

See Also
--------

- `getfacl(1) - Linux man page <https://linux.die.net/man/1/getfacl>`_

- `setfacl(1) - Linux man page <https://linux.die.net/man/1/setfacl>`_

- `Arch Linux - Access Control Lists <https://wiki.archlinux.org/index.php/Access_Control_Lists>`_
