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

    > Filenames that start with "**.**" are hidden, you can view them however with the ls command and pass the "**-a**" flag to it ("a" for all).
    
    ```
    ls -a
    ```
    > Another useful flag is "**-l**" ("l" for long). This shows a detailed list of files in a long format. This will show you detailed information, starting from the left: 
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

- ___less___: This command is useful for text files larger than a simple output. The text is displayed in a paged manner, so you can navigate through a text file page by page.
    Some of the options when navigating through ___less___ are:
    ```
    q: Used to quit out of less and go back to your shell.
    Page up, Page down, Up and Down: Navigate using the arrow keys and page keys.
    g: Moves to beginning of the text file.
    G: Moves to the end of the text file.
    /: You can search for specific text inside the text document. Prefacing the words you want to search with /, for example: /trabajo
    h: If you need a little help about how to use less while you’re in less, use help.
    ```
- ___history___: This command shows up a list with all the commands you previously entered.
    >Want to run the same command you did before, just hit the **up arrow**.
    >
    > Want to run the previous command without typing it again? Use **!!**. If you typed cat file1 and want to run it again, you can actually just go **!!** and it will run the last command you ran.
    >
    > Another history shortcut is **ctrl-R**, this is the ___reverse search___ command, if you hit ctrl-R and you start typing parts of the command you want it will show you matches and you can just navigate through them by hitting the **ctrl-R** key again. Once you found the command you want to use again, just hit the Enter key.
- ___cp___: This command is used for copying files.

    - Here, *Gilligan_250519.txt* is the file you want to copy and *New_directory/* is the path where you are copying the file to.

        ```
        cp Gilligan_250519.txt New_directory/
        ```

    - You can copy multiple files and directories as well as use wildcards. A wildcard is a character that can be substituted for a pattern based selection, giving you more flexibility with searches. You can use wildcards in every command for more flexibility.

        > __*__: the wildcard of wildcards, it's used to represent all single characters or any string.
        >
        > __?__: it is used to represent one character.
        >
        > __[ ]__: it is used to represent any character within the brackets.

        For example:
        ```
        cp *.jpg /home/pete/Pictures
        ```
        This will copy all files in your current directory with the *.jpg* extension to the *Pictures* directory.

    - Another useful command is to use the ___-r___ flag. This will recursively copy the files and directories **within a directory**. If you try to do a _cp_ on a directory that contains a couple of files to another directory it won't work because **you’ll need to copy over the files and directories inside as well** with ___-r___.
        ```
        $ cp -r Pumpkin/ /home/pete/Documents
        ```
    
    > Note: If you copy a file over to a directory that has the same filename, the file will be overwritten with whatever you are copying over. You can use the -i flag (interactive) to prompt you before overwriting a file. For example:
        ```
        $ cp -i mycopiedfile /home/pete/Pictures
        ```
- ___mv___: This command is used for **moving files** and also **renaming** them.
    - You can rename files like this:
        ```
        $ mv oldfile newfile
        ```

    - Or you can actually move a file to a different directory:
        ```
        $ mv file2 /home/pete/Documents
        ```

    - And move more than one file:
        ```
        $ mv file_1 file_2 /somedirectory
        ```

    - You can rename directories as well:
        ```
        $ mv directory1 directory2
        ```

    - If you move a file or directory it will overwrite anything in the same directory. So you can use the ***-i*** flag to prompt you before overwriting anything.
        ```
        mv -i directory1 directory2
        ```

    - Let’s say you did want to move a file to overwrite the previous one. You can also make a backup ***-b*** of that file and it will just rename the old version with a **~**.
        ```
        $ mv -b directory1 directory2
        ```
        ![interactive and backup arguments](interactive and backup arguments.png)

- ___mkdir___: This command (Make Directory) is useful for creating new directories. It will create a directory if it doesn’t already exist, and you can even make multiple directories at the same time.
    ```
    $ mkdir books paintings
    ```
    You can also create subdirectories at the same time with the -p (parent) flag.
    ```
    $ mkdir -p books/hemmingway/favorites
    ```
