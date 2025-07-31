## System logging
The **services**, **kernel**, ***daemons*** (1), etc. on our system are constantly doing something, and this data is actually sent to be saved on our system in the form of ***logs***. This allows us to have a readable journal of the events that are happening on our system. 

This data is usually kept in the ***/var*** directory. The ***/var*** directory is where we keep our variable data, such as ***logs***. A service called ***syslog*** sends this information to the ***system logger***.

**Syslog** actually contains many components, one of the most important ones is a daemon running called ***rsyslogd***, that ***waits for event mesagges to occur and filter the ones it wants to know about***. Depending on what it's supposed to do with that message, it will send it to a file, send it to the console or do nothing with it.

Here is an example of a line from ***syslog***:
```
$ less /var/log/syslog

Jan 27 07:41:32 icebox anacron[4650]: Job `cron.weekly' started
```
Here we can see that at *Jan 27 07:41:32* our cron service ran the *cron.weekly* job.

> We can view all the event messages that syslog collects in the **/var/log/syslog** file.

---
## (1) Daemons
In Linux, a ***daemon*** is a computer program that runs continuously in the background, independent of direct user interaction or a controlling terminal. Daemons are essential for the operation of many system services and functionalities.

<u> **Key characteristics of daemons:** </u>

> - **Background execution**: They operate in the background, performing tasks without requiring an active user session or a graphical interface.
>
> - **No controlling terminal**: Unlike regular user-launched applications, daemons typically do not have a controlling terminal associated with them. This means they cannot directly interact with a user through input/output.
>
> - **System services**: Many daemons provide core system services, such as:
>   - **Network services**: ***sshd*** (SSH daemon) for remote access, ***httpd*** (Apache web server daemon) for serving web content.
>   - **System management**: ***syslogd*** for system logging, ***cron*** for scheduling tasks.
>   - **Resource management**: Daemons that manage hardware resources or system processes.
>
> - **Persistent operation**: Daemons are designed to run continuously, often starting automatically at boot time and remaining active as long as the system is running.
> - **Naming convention**: In Unix-like systems, daemons are often named with a "**d**" suffix (e.g., *sshd*, *syslogd*, *httpd*).

In essence, daemons are the silent workhorses of a Linux system, providing the underlying services and functionalities that allow users and other programs to operate effectively.

---

