- ___echo___: The _echo_ command just prints out the text arguments to the display.
    ```
    $ echo Hello World
    Hello World
    ```

- ___path___: This command means “print working directory” and it just shows you which directory you are in.

- ___cd___: This command mens "change directory" and it helps us change to the directory we want to go. 
    > There are two different ways to specify a path, with absolute and relative paths.
    > - _Absolute path_: This is the path from the root directory. The root is the head honcho. The root directory is commonly shown as a slash. Every time your path starts with "/" it means you are starting from the root directory. For example, "/home/pete/Desktop".
    >
    > - _Relative path_: This is the path from where you are currently in filesystem. If I was in location "/home/pete/Documents" and wanted to get to a directory inside "Documents" called "taxes", I don’t have to specify the whole path from root like "/home/pete/Documents/taxes", I can just go to "taxes/" instead.

    **Some shortcuts:**
    ```
    $ cd . (current directory): This is the directory you are currently in.

    $ cd .. (parent directory): Takes you to the directory above your current.

    $ cd ~ (home directory). This directory defaults to your “home directory”

    $ cd - (previous directory): This will take you to the previous directory you were just at.
    ```

- ___ls___: This command means "list directories" and it will list directories and files in the current directory by default, however you can specify which path you want to list the directories of.

    > Filenames that start with "**.**" are hidden, you can view them however with the ls command and pass the "**-a**" argument to it ("a" for all).
    
    ```
    ls -a
    ```
    > Another useful argument is "**-l**" ("l" for long). This shows a detailed list of files in a long format. This will show you detailed information, starting from the left: 
    >- file permissions,
    >- number of links,
    >- owner name,
    >- owner group,
    >- file size,
    >- timestamp of last modification,
    >- file/directory name. 
    
    ```
    pete@icebox:~$ ls -l

    total 80

    drwxr-x--- 7 pete penguingroup   4096 Nov 20 16:37 Desktop

    drwxr-x--- 2 pete penguingroup   4096 Oct 19 10:46  Documents

    drwxr-x--- 4 pete penguingroup   4096 Nov 20 09:30 Downloads

    drwxr-x--- 2 pete penguingroup   4096 Oct  7 13:13   Music

    drwxr-x--- 2 pete penguingroup   4096 Sep 21 14:02 Pictures

    drwxr-x--- 2 pete penguingroup   4096 Jul 27 12:41   Public

    drwxr-x--- 2 pete penguingroup   4096 Jul 27 12:41   Templates

    drwxr-x--- 2 pete penguingroup   4096 Jul 27 12:41   Videos
    ```
    > We can even add both arguments together using "**-la**" or "**-al**". The order of the arguments determines which order it goes in, most of the time this doesn’t really matter.

    > Another useful arguments are:
    >- **ls -R**: recursively list directory contents.
    >- **ls -r**: reverse order while sorting.
    >- **ls -t**: sort by modification time, newest first.

- ___touch___: This command allows you to the create new empty files.

- ___file___: This command will show you a description of the file’s contents, including the file extension.

- ___cat___: It stands for "concatenate", and it not only displays file contents but it can combine multiple files and show you the output of them. It’s not great for viewing large files and it’s only meant for short content.