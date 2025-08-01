## stdout (Standard Out)
### echo
Processes use I/O streams to receive input (I) and return output (O). By default, the ***echo*** command takes the **input** (**standard input** or **stdin**) from the keyboard and returns the **output** (**standard output** or **stdout**). So that's why when you type "Hello world!" in your shell, you get "Hello world!" on hte screen. However, I/O redirection allows us to change this default behavior.

### > & >> operators
The **'>'** is a **redirection operator** that allows us to change where the standard output goes. It allows us to send the output of ```$ echo Hello world!``` to a file instead of the screen. If the file does not already exist, it will create it for us. However, if it does exist ***it will overwrite the content of the file***.

In case we don't want to overwrite the original file, we can use the **'>>' redirection operator**. ***It will append the input to the end of the file***. If the file does not exist, it will also create it for us.

> Example:
>```
> $ ls -l /var/log > myOutput.txt
>
> $ tail myOutput.txt
>
> -rw-rw-r--  1 root      utmp                 0 Feb 15 05:09 lastlog
>drwx------  2 root      root              4096 Feb 15 05:09 private
>-rw-r-----  1 syslog    adm             933131 Aug  1 01:20 syslog
>-rw-r-----  1 syslog    adm             234793 Jul  9 19:02 syslog.1
>```

## stdin (Standard In)
We can use different standard input streams, we can use **stdin** from *keyboards*, from *files*, *outputs from other processes* and the *terminal* as well. To do this we use the **'<' redirection operator**.

**Example**:
> ```
> $ echo "A continuación voy a añadir el texto que se encuentra en el archivo 'myTextArchive.txt' al archivo 'banana.txt':" > banana.txt
>
> $ cat < myTextArchive.txt >> banana.txt
>
> $ echo "Ahora, debajo de esta línea, tendría que poder añadir el texto del archivo 'editedFile.txt':" >> banana.txt
>
> $ cat < editedFile.txt >> banana.txt
>
> $ echo "Esta última línea es para demostrar que el operativo fue todo un éxito y pude añadir cada párrafo a continuación del siguiente sin ningún tipo de problema. Con ayuda de los operadores '<', '>' y '>>'. Este archivo sirve de demostración para la lección de 'stdin' y 'stdout' de la página 'LinuxJourney'" >> banana.txt
>
> $ echo "
> *********
>
> Esta es una prueba con para hacer una separación en párrafos y dejar un espacio extra al final utilizando 'shift + Enter' para realizar los saltos de línea.
>
> ---- Fin. ----
>
> " >> banana.txt
>
>> $ less banana.txt
>```

> Normally in the ***cat*** command, we use a file as stdin. In this case, we **redirected both** *myTextArchive.txt* and *editedFile.txt* **to be our *stdin* in each case**. Then **the output of those operations (the contents of both files) gets redirected** to a new file named *banana.txt*. 
>
> This way we did sort of a copy of their contents into another file just using the redirection operators.

## pipe and tee
The **|** (*pipe operator*) allows us to **get the *stdout* of a command and make it the *stdin* of another process**. For example:

```
$ ls -la /etc | less
```

In this case, we took the ***stdout*** of '*ls -la /etc*' and then ***piped*** it to the ***less*** command.

And if we want to write that output into a specific file as well as seeing it on the screen, we can use the ***tee command***.

```
$ ls -la /etc | tee myListFile.txt
```
In this case, **the output will create and/or overwrite the file with the same information presented on the screen**.

## env (Environment)
This outputs a whole lot of information about the environment variables you currently have set. These variables contain useful information that the shell and other processes can use.

**Example:**
```
$ env

$ echo $USER

$ echo $HOME

$ echo $PATH
```
#### The **$PATH environment variable**

One particularly important variable is $PATH. It returns a list of paths separated by a colon.

```
$ echo $PATH

/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games
```
**It tells the system in which directories to look for the executable programs (also called ***binaries***) when we type a command in the terminal**. So, it can be translated as: "When I write a command, look for it in these directories, in that order, and execute it when found".

In case we install a program manually and store it in a personal directory (for example '*/home/desktop/downloads*'), **the system won't find it when trying to execute it** and the terminal will return ``` command not found ```. The reason why this happens is because **our personal directory is not in the $PATH variable, so the system will never try to look for it in there**.

The way to solve this is by adding our personal folder to the $PATH variable with the following command:
```
export PATH=$PATH:/home/desktop/downloads
```
> **Why $PATH is important?**
>
> - It **facilitates the execution of commands** without having to write complete paths.
> - It is **key for the system to know how and where to find installed programs**.
> - We can **personalize it for our own tools without corrupting the others**.


