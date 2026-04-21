## Files and Permissions
### Modifying permissions in Linux

**Original access permission:** -rw-r--r-- 1 m3talh3ad m3talh3ad 31 Aug  6 04:38 file1.txt
1) ``$ chmod 600 file1.txt``

    **Result:** -rw------- 1 m3talh3ad m3talh3ad 31 Aug  6 04:38 file1.txt
2) ``$ chmod 755 file1.txt``
    
    **Result:** -rwxr-xr-x 1 m3talh3ad m3talh3ad 31 Aug  6 04:38 file1.txt
3) ``$ chmod 644 file1.txt``
    
    **Result:** -rw-r--r-- 1 m3talh3ad m3talh3ad 31 Aug  6 04:38 file1.txt
4) ``$ chmod 654 file1.txt``
    
    **Result:** -rw-r-xr-- 1 m3talh3ad m3talh3ad 31 Aug  6 04:38 file1.txt
5) ``$ chmod 644 file1.txt``
    
    **Result:** -rw-r--r-- 1 m3talh3ad m3talh3ad 31 Aug  6 04:38 file1.txt
------------------------------------
The numerical representations are seen below:
 - **4**: read permission
 - **2**: write permission
 - **1**: execute permission
____________________________________

***CASE OF USE:***
In the second example (chmod 755), we are combining all the permissions into one number:
 - 7 = 4 + 2 + 1, so 7 is the user permissions and it has read, write and execute permissions.
 - 5 = 4 + 1, the group has read and execute permissions.
 - 5 = 4 + 1, and all other users have read and execute permissions.