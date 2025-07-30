#### System logging
, kernel, daemons, etc. on our system are constantly doing something, and this data is actually sent to be saved on our system in the form of ***logs***. This allows us to have a readable journal of the events that are happening o our system. Thiks data is usually kept in the ***/var*** directory. The ***/var*** directory is where we keep our variable data, such as ***logs***. A service called ***syslog*** sends this information to the ***system logger***.

**Syslog** actually contains many components, one of the most important ones is a daemon running called ***rsyslogd***, that waits for event mesagges to occur and filter the ones it wants to know about. Depending on what it's supossed to do with that message, it will send it to a file, send it to the console or do nothing with it.

Here is an example of a lione from ***syslog***:
```
$ less /var/log/syslog

Jan 27 07:41:32 icebox anacron[4650]: Job `cron.weekly' started
```
Here we can see that at *Jan 27 07:41:32* our cron service ran the *cron.weekly* job.

> We can view all the event messages that syslog collects in the **/var/log/syslog** file.

