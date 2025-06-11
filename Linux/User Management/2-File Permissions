### File permissions
```
$ ls -l Desktop/
drwxr-xr-x 2 pete penguins 4096 Dec 1 11:45 .
```
There are four parts to a file's permissions.
```
d | rwx | r-x | r-x 
```
- The first part is the filetype, which is denoted by the first character in the permissions, in our case since we are looking at a directory it shows ***d*** for the filetype. Most commonly you will see a ***-*** for a regular file.
- The next three parts of the file mode are the actual permissions. The permissions are grouped into 3 bits each:
    - The first 3 bits are ***user permissions***,
    - the next 3 are ***group permissions*** and
    - the last 3 are ***other permissions***.

Each character represent a different permission:
- **r**: readable
- **w**: writable
- **x**: executable (basically an executable program)
- **-**: empty

So in the above example, we see that the user *pete* has read, write and execute permissions on the file. The group *penguins* has read and execute permissions. And finally, the *other* users (everyone else) has read and execute permissions.

### Modifying permissions
This is done with the **chmod** command.
- First, select which permission set you want to change: **u** (user), **g** (group) or **o** (other).
- Then add or remove permissions with a **+** or **-** character.

#### Adding permissions
```
chmod u+x myFile
```
The above command reads like this: "change permission on *myFile* by adding executable permission bit on the *user* set". So now the user has executable permission on this file!

#### Removing permissions
```
chmod u-x myFile
```

#### Adding multiple permissions
```
chmod ug+w
```
##### Adding multiple permissions with numbers
This method allows you to change permissions all at once. Instead of using r, w, or x to represent permissions, you'll use a **numerical representation** for a single permission set. So no need to specify the group with g or the user with u.

The numerical representations are seen below:
 - **4**: read permission
 - **2**: write permission
 - **1**: execute permission

Let's look at an example:
```
chmod 755 myFile
```
755 covers the permissions for all sets. The first number (7) represents *user permissions*, the second number (5) represents *group permissions* and the last 5 represents *other permissions*.
Here we are combining all the permissions into one number now, so you'll have to get some math involved.
 - 7 = 4 + 2 + 1, so 7 is the user permissions and it has read, write and execute permissions
 - 5 = 4 + 1, the group has read and execute permissions
 - 5 = 4 +1, and all other users have read and execute permissions

> **NOTE**: You must sum up all the permissions that you want each set to have. If a set has write permissions and you want to add read permissions, if you just use the number 4, for example, the set will only have read permissions and all other permissions will be overwritten. So, to add both permissions you must use the number 6 (read + write permissions).

### Ownership permissions
You can also modify the group and user ownership of the file as well.
#### Modify user ownership
```
sudo chown william myFile
```
This command will set the owner of myFile to william.

#### Modify group ownership
```
$ sudo chgrp elGroup myFile
```
This command will set the group of myFile to elGroup.

#### Modify both user and group ownership at the same time 
```
$ sudo chown william:elGroup myFile
```
If you add a colon and groupname after the user you can set both the user and group at the same time.

### Umask
Every file that gets created comes with a default set of permissions. If you ever wanted to change that default set of permissions, you can do so with the ***umask*** command. This command takes the 3 bit permission set we see in numerical permissions but, instead of adding these permissions, ***umask* takes away these permissions**.
```
umask 021
```
> In the above example, we are stating that we want the default permissions of new files to **allow users access to everything**, but **for groups we want to take away their write permission** and **for others we want to take away their executable permission**.

The default umask on most distributions is 022, meaning all user access, but no write access for group and other users.

When you run the *umask* command it will give that default set of permissions on any new file you make. However, if you want it to persist you'll have to modify your startup file (.profile).

### Set User ID (SUID)
There are many cases in which normal users need elevated access to do stuff. The system administrator can't always be there to enter in a root password every time a user needed access to a protected file, so there are special file permission bits to allow this behavior.
> The Set User ID (SUID) allows a user to run a program as the owner of the program file rather than as themselves.

For example, the ***passwd*** command allows you to change your password. We know that passwords are saved in the */etc/shadow* file, and it can only be modified by the root user. However, a normal user can execute this command and modify his own password. This can be possible because the executable ***/usr/bin/passwd*** has the **SUID bit activated**. When a file has this permission set, it allows the users who launched the program to get the file owner's permission as well as execution permission as if they were the root user.

How to see this in the terminal?
```
$ ls -l /usr/bin/passwd
-rwsr-xr-x 1 root root 54256 Jan 1 12:34 /usr/bin/passwd
```
The key is in the ***s*** instead of the ***x*** in the owner user permissions (rws). This indicates that it has the SUID activated.

#### Modifying SUID
Just like regular permissions there are two ways to modify SUID permissions.

*Symbolic way*:
```
$ sudo chmod u+s myfile
```

*Numerical way*:
```
 sudo chmod 4755 myfile
```
As you can see the SUID is denoted by a 4 and pre-pended to the permission set. You may see the SUID denoted as a capital S this means that it still does the same thing, but it does not have execute permissions.

### Set Group ID (SGID)
There is a set group ID (SGID) permission bit. This bit allows a program to run as if it was a member of that group. For example:

```
$ ls -l /usr/bin/wall
-rwxr-sr-x 1 root tty 19024 Dec 14 11:45 /usr/bin/wall
```
Here we can see that the permission bit is in the group permission set.

#### Modifying SGID
*Symbolic way*:
```
$ sudo chmod g+s myfile
```

*Numerical way*:
```
$ sudo chmod 2555 myfile
```
The numerical representation for SGID is 2.

### Process Permissions
When you run the ***passwd*** command with the SUID permission bit enabled you will run the program as root, however this does't mean that, since you are temporarily root, you can modify other user's passwords. This is because of the many UIDs that Linux implements. There are three UIDS associated with every process:
- **Effective User ID**: This UID is used to grant access rights to a process. When you launch a process, it runs with the same permissions as the user or group that ran it. So, if a user ran the *touch* command, the process would run as him and any files he created would be under his ownership.
- **Real User ID**: This is the ID of the user that launched the process. These are used to track down who the user who launched the process is.
- **Saved User ID**: This allows a process to switch between the ***effective UID*** and ***real UID***, and vice versa. This is useful because we don't want our process to run with elevated privileges all the time, it's just good practice to use special privileges at specific times.

Example:
> When running the ***passwd*** command, your **effective UID** is your user ID, let's say its 500 for now. Remember the ***passwd*** command has the SUID permission enabled. So when you run it, your effective UID is now 0 (0 is the UID of root). Now this program can access files as root.
>
> Let's say you get a little taste of power and you want to modify Sally's password, Sally has a UID of 600. Well you'll be out of luck, fortunately the process also has your **real UID** in this case 500. It knows that your UID is 500 and therefore you can't modify the password of UID of 600. (This of course is always bypassed if you are a superuser on a machine and can control and change everything).
>
> Since you ran ***passwd***, it will start the process off using your **real UID**, and it will save the UID of the owner of the file (**effective UID**), so you can switch between the two. No need to modify all files with root access if it's not required.

Most of the time the **real UID** and the **effective UID** are the same, but in such cases as the ***passwd*** command they will change.

### The Sticky Bit
This permission bit "sticks a file/directory", this means that only the owner or the root user can delete or modify the file. This is very useful for shared directories.

Take a look at the example below:
```
$ ls -ld /tmp
drwxrwxrwxt 6 root root 4096 Dec 15 11:45 /tmp
```
You'll see a special permission bit at the end here **t**, this means everyone can add files, write files, modify files in the ***/tmp*** directory, but only root can delete the ***/tmp*** directory.

#### Modifying sticky bit
```
$ sudo chmod +t mydir

$ sudo chmod 1755 mydir
```
The numerical representation for the sticky bit is **1**.