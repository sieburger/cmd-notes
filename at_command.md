# at command

Below example will schedule “sh backup.sh” command to be executed on next 9:00 AM once.
```sh
at 9:00 AM
at> sh backup.sh
at> ^d
job 3 at 2013-03-23 09:00
```
Use ^d to exit from at prompt.
You can also use the following option to schedule a job. The below command will run “sh backup.sh” at 9:00 in the morning.

`echo "sh backup.sh" | at 9:00 AM`

When we list jobs by root account using `atq`, it shows all users jobs in the result. But if we execute it from a non-root account, it will show only that users jobs.
```sh
atq

3       2013-03-23 09:00 a root
5       2013-03-23 10:00 a rahul
1       2013-03-23 12:00 a root
```

You can remove any at job using `atrm` with their job id.
```sh
atrm 3
atq

5       2013-03-23 10:00 a rahul
1       2013-03-23 12:00 a root
```

I.E.
```sh
magi@bbplay:~$ date
Tue Oct 22 18:22:17 UTC 2019
magi@bbplay:~$ echo sh m-minerd.sh | at 6:26 PM
warning: commands will be executed using /bin/sh
job 7 at Tue Oct 22 18:26:00 2019
```
***


ref:
https://tecadmin.net/one-time-task-scheduling-using-at-commad-in-linux/

