.. _acl:

File and Directory Access Control List (ACL)
============================================

Default ownership and permissions are modified to address the issue of
unintentional overly broad grants of directory permissions.

Filesystem ACL change restriction defaults

-  Default ACL for new file creation is 600 instead of 644 (**default
   umask changing from 022 to 077**)
-  All **top level folders will not permit ACL changes by users** (home,
   projects)
-  Though ACL expansion of subfolders isn't permitted by default, a
   **service request can be made to enable either ACL self management or
   a specific ACL change enabled by administrators**.
-  Recommended practice:

   -  Use projects directory to share within project account members.
   -  Expand access only to *what* you intend to *whom* you intend.
      chmod is allowed, but setfacl is preferred.
   -  Periodically review your file and folder permissions (getfacl
      shows all extended attributes)

.. _acl-home-dir:

Home Directories
----------------

Default home directories will have the following setting shown below.
Note that root is both owner and group, and the '+' indicates additional
attributes are present; in the example below, extended attributes for
ACLs are enabled. Full ACL listing can be queried with the getfacl
command as shown. Note: *The Posix representation of the top level
directory ACL represents a "calculated effective mask" of 770
(drwxrwx---+), because additional extended attributes grant rwx to
another user, in this case, "username". This can be interpreted exactly
like a mask of 700 for user username.*

:: 

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

Project directories will have similar restrictions as home, with the
exception that files here will be group accessible (will override
umask). The respective project group will own files created in the
project directory by default, overriding the user primary group if it
differs.

.. _enabling_acl:

Enabling ACL Modification (if needed)
-------------------------------------

*Enabling access to others in the same group*

Use your project space (/projects/psn) if you are sharing with others in
your same project. This is what the space is designed for. Please submit
a service request with any exceptions to be evaluated.

*Enabling access to others outside of a group*

To enable access to directories and files residing within your home
directory you need to:

#. Submit a ticket asking for an "ACL change request"  



.. 
   `ACL service

.. 
   request <mailto:help%2Bhydro@ncsa.illinois.edu?       subject=Request%20for%20ACL%20change&body=%3CSUBSTITUTE_ALL_CAPS_TEXT%3E%0AAs%20part%20of%20this%20ACL%20change%20request%2C%20I%20understand%20and%20do %20not%20object%20to%20an%20administrator%20altering%20existing%20Posix%20ACLs%20from%20first-level%20directory%20contents%20(non-  recursive)%20by%20issuing%20a%20%22chmod%20og-  rwx%20%3CTOP_LEVEL_DIRECTORY%3E%2F*%22.%20Existing%20extended%20ACL%20attributes%20on%20directory%20contents%20are%20already%20presumed%20intentional%20 and%20will%20not%20be%20modified%20by%20the%20admin.%0AI%20%5B%20need%20%7C%20do%20not%20need%20%5D%20additional%20guidance%20on%20ACL%20management%20be st%20practices.%0A%0AOption%20A%3A%20(Please%20do%20it%20for%20me)%0AI%20am%20requesting%20ACL%20expansion%20to%20%3CDIRECTORY%3E%20to%20%3CUSER%2C%20GR OUP%2COTHER%3E%20with%20%3CR%7CW%7CX%3E%20permissions.%20(list%20full%20request)%0A...%0A%0AOption%20B%3A%20(Self-   Managed)%0AI'll%20manage%20my%20ACLs.%20Please%20enable%20traversal%20into%20%3CTOP_LEVEL_DIRECTORY%3E%20for%20me.%0AI%20understand%20that%20this%20will %20expose%20all%20data%20in%20my%20directory%20according%20to%20the%20permissions%20I%20grant%2C%20and%20I%20will%20take%20care%20not%20to%20grant%20unn ecessarily%20broad%20access.%0A>`__


with the top level folder you wish to be traverseable, and by whom.
e.g. I would like my group "X" to be able to have read and write
access to a subdirectory of my home directory. 
   
..    
   The link includes a
   template request.

#. Depending on the request, an admin will either:

   -  set a specific ACL grant as requested
   -  set the top level to an effective 701 permission, (drwx-----x ).
      This will allow traversal into your top-level directory by anyone
      on the system to access any file or folder according to its own
      specific permission limitations.

#. An admin will check for any custom umask setting in your local
   environment setup that may result in unintentional data exposure in
   combination with requested ACL changes.
#. If self-managed, begin modifying ACLs on desired subfolders using
   chmod or setfacl. setfacl is strongly preferred due to its ability to
   be much more specific with user/group/mask combinations. Support
   staff can provide any additional best practice guidance requested to
   help you configure ACL layouts that serve your objective.

*To enable access for a specific user from another group to a file or
directory*

Below is an example where user1 adds read access to a file for user2
using setfacl and then checking the permissions using getfacl. Note that
the permissions for the parent directory need to allow for "o+x" as
mentioned above.

:: 

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


Below is an example where user1 adds read+execute access to a directory
for user2 using setfacl and then checking the permissions using getfacl.
Note that the permissions for the parent directory need to allow for
"o+x" as mentioned above.

::

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

`getfacl(1) <https://linux.die.net/man/1/getfacl>`__

`setfacl(1) <https://linux.die.net/man/1/setfacl>`__

`Access Control
Lists <https://wiki.archlinux.org/index.php/Access_Control_Lists>`__
