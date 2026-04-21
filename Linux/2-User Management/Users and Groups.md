### Users and Groups
In any traditional operating system, there are users and groups. They exist solely for access and permissions.
**Each user has their own home directory** where their user specific files get stored, this is usually located in */home/username*, but can vary in different distributions.

The system uses **user ids (UID)** to manage users. Usernames are the friendly way to associate users with identification, but the system identifies users by their UID. The system also uses **groups** to manage permissions. Groups are just sets of users with permission set by that group, they are identified by the system with their **group ID (GID)**.

### Root
In Linux, one of the most important users is **root or superuser**. ***Root is the most powerful user on the system, it can access any file and start and terminate any process***. For that reason, it can be dangerous to operate as root all the time, you could potentially remove system critical files.
> If root access is needed and a user has not it, they can run a command as root instead with the _sudo command_. The **sudo command (superuser do)** is used to run a command with root access.

> There is a file called the ***/etc/sudoers*** file, this file lists users who can run *sudo*. You can edit this file with the **visudo** command.

### Password management file: *etc/passwd*
To find out **what users are mapped to what ID**, look at the ***/etc/passwd*** file.
```
$ cat /etc/passwd
```
This file shows you a list of users and detailed information about them. For example, the first line in this file most likely looks like this:
```
root:x:0:0:root:/root:/bin/bash
```
Each line displays user information for one user, most commonly you'll see the root user as the first line. There are many fields separated by colons that tell you additional information about the user, let's look at them all:

>    1- **Username**
>
>    2- **User's password**: The password is not really stored in this file, it's usually encrypted stored in the ***/etc/shadow*** file. You can see many different symbols that are in this field, if you see an **"x"** that means the password is stored in the ***/etc/shadow*** file, a __"*"__ means the _user doesn't have login access_, and if there is a **blank field** that means the _user doesn't have a password_.
>
>    3- **The user ID**: As you can see root has the UID of 0
>
>    4- **The group ID**
>
>    5- **GECOS field**: This is used to generally leave comments about the user or account such as their real name or phone number, it is comma delimited.
>
>    6- **User's home directory**
>
>    7- **User's shell**: You'll probably see a lot of user's defaulting to bash for their shell.

> You'll notice ***/etc/passwd*** contains other users. **Remember that users are really only on the system to run processes with different permissions.** Sometimes we want to run processes with pre-determined permissions.

> Also should note that you can **edit** the ***/etc/passwd*** file by hand if you want to add users and modify information with the **vipw** tool.

### User authentication file: *etc/shadow*
The ***/etc/shadow*** file is used to store **information about user authentication**. It requires superuser read permissions.
```
$ sudo cat /etc/shadow
```
You'll notice that it looks very similar to the contents of ***/etc/passwd***, however in the password field you'll see an encrypted password. The fields are separated by colons as followed:
>    1- **Username**
>
>    2- **Encrypted password**
>
>    3- **Date of last password changed**: Expressed as the number of days since Jan 1, 1970. If there is a 0 that means the user should change their password the next time they login
>
>    4- **Minimum password age**: Days that a user will have to wait before being able to change their password again
>
>    5- **Maximum password age**: Maximum number of days before a user has to change their password
>
>    6- **Password warning period**: Number of days before a password is going to expire
>
>    7- **Password inactivity period**: Number of days after a password has expired to allow login with their password
>
>    8- **Account expiration date**: Date that user will not be able to login
>
>    9- **Reserved field** for future use

> In most distributions today, user authentication doesn't rely on just the ***/etc/shadow*** file, there are other mechanisms in place such as **PAM (Pluggable Authentication Modules)** that replace authentication.

### Groups management file: *etc/group*
Another file that is used in user management is the ***/etc/group*** file. This file has the information for different groups with different permissions.
```
$ cat /etc/group
```
The ***/etc/group*** fields are as follows:

>    1- **Group name**
>
>    2- **Group password**: There isn't a need to set a group password, using an elevated privilege like sudo is standard. A __"*"__ will be put in place as the default value.
>
>    3- **Group ID (GID)**
>
>    4- **List of users**: You can manually specify users you want in a specific group.

### User Management Tools: *adduser, addgroup, usermod*
Most enterprise environments are using management systems to manage users, accounts and passwords. However, on a single machine computer there are useful commands to run to manage users.

- **Adding groups**: You can add groups by using the **addgroup** command.
    ```
    sudo addgroup grupo_prueba
    ```

- **Adding Users**: You can use the **adduser** command. It will ask for a *new password* for the new user, as well as a *password confirmation*. This command also contains more helpful features, such as making a home directory and completing user information (full name, room number, phone number, etc.).
    ```
    $ sudo adduser rodolfo
    ```
    This command creates an entry in ***/etc/passwd*** for *rodolfo*, sets up default groups and adds an entry to the ***/etc/shadow*** file.

     There are configuration files for adding new users that can be customized depending on what you want to allocate to a default user.
    
- **Adding user to a group**: To add a user into a specific group you can use the **--ingroup** option within the ***adduser*** command.
    ```
    sudo adduser usuario_prueba --ingroup grupo_prueba
    ```
    ![Adding user into a specific group](/Linux/2-User%20Management/Adding%20user%20to%20group.png)

- **Removing users**: To remove a user, you can use the **userdel** command.
    ```
    $ sudo userdel rodolfo
    ```
    This basically does its best to undo the file changes by useradd.

- **Changing Passwords**: The ***passwd*** command will allow you to change the password of yourself or another user (if you are root).
    ```
    $ passwd rodolfo
    ```

- **Adding users to secondary groups**: We can do this by using the ***usermod*** command with the -aG options.
    - **-G**: specifies the new list of secondary groups.
    - **-a**: stands for "append" and it is a very important option. It adds the user to the specified group(s) ***without removing*** them from their current groups. If you omit this option, the user will be removed from all other secondary groups not listed in the command.

- **Group affiliations**: The **groups** command provides a clean one-line summary of the groups to which the given user belongs to.
    ```
    $ groups usuario_prueba

    usuario_prueba : grupo_prueba users
    ```
    In this output, the name before the collon is the user being queried. The list after the colon, shows all the groups. The first one is the ***primary group***, and all the subsequent ones are the ***secondary groups***.

- **Group deletion**: To delete a group, we use the **groupdel** command. It's ***important*** to note that ***you cannot delete the primary group of an existing user. You must first change the user's primary group before deleting the old one***. When successful, the command will not produce any output. It simply removes the group's entry from the system's group database, primarily the ***/etc/group*** file.