### Processes (ps)
Processes are the programs that are running on your machine. They are managed by the kernel and each process has an ID associated with it called the ***Process ID (PID)***. This **PID** is assigned in the order that processes are created.

```
$ ps
```
This command shows a quick snapshot of the current processes:
- **PID**: Process ID
- **TTY**: Controlling terminal associated with the process
- **STAT**: Process status code
- **TIME**: Total CPU usage time
- **CMD**: Name of executable/command

```
$ ps aux
```
The **a** displays all processes running, including the ones being ran by other users. The **u** shows more details about the processes. The **x** lists all processes that don't have a TTY associated with it. These programms will show a **?** (question mark) in the TTY field, and they are most common in daemon processes that launch as part of the system startup.

Some other fields are:
- USER: The effective user (the one whose access we are using)
- PID: Process ID
- %CPU: CPU time used divided by the time the process has been running
- %MEM: Ratio of the process's resident set size to the physical memory on the machine
- VSZ: Virtual memory usage of the entire process
- RSS: Resident set size, the non-swapped physical memory that a task has used
- TTY: Controlling terminal associated with the process
- STAT: Process status code
- START: Start time of the process
- TIME: Total CPU usage time
- COMMAND: Name of executable/command

Another very useful command is the **top** command, it gives you real time information about the processes running on your system instead of a snapshot. By default you´ll get a refresh every 10 seconds. It is an extremely useful tool to see what processes are taking up a lot of your resources.
```
$ top
```

### Controlling terminal
The TTY is the terminal that executed the command.
There are two types of terminals:
- **Regular terminal devices**: A native terminal device that you can type into and send output to your system. It is not the same as the terminal you've been using to get your shell.
- **Pseudoterminal devices**: It is what you've been using to working in. They emulate terminals with the shell terminal window and are denoted by PTS. If you look at **ps** again, you'll see your shell process under _pts/*_.

Processes are usually bound to a controlling terminal. For example, if you were running a program on your shell window such as ***find*** and you closed the window, your process would also go with it.

There are processes such as ***daemon processes***, which are special processes that are essentially keeping the system running. They often start at system boot and usually get terminated when the system is shutdown. They run in the background and since we don't want these special processes to get terminated they are not bound to a controlling terminal. In the ps output, the TTY is listed as a **?** meaning it does not have a controlling terminal.


### Process details
A process is a running program on the system. More precisely, it is the system allocating memory to make the program run.

The kernel is in charge of processes, when we run a program the kernel loads up the code of the program in memory, determines and allocates resources and then keeps tabs on each process, it knows:
- The status of the process
- The resources the process is using and receives
- The process owner
- Signal handling
- And basically everything else

It's the kernel's job to make sure that processes get the right amount of resources depending on process demands. When a process ends, the resources it used are now freed up for other processes.

### Process creation
