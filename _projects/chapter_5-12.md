---
title: 'Learning Linux - Chapter 5: Section 12'
description: 'This section introduces and explains the terms Application, Script, Process, Daemon, Thread and Job. These will be described in more detail in the following sections.'
date: 2022-01-01 05:12:00
featured_image: 'mT68055%25%25--tYF_5__5jhhh5pls$0-G.jpeg'
gallery_images: 'YtOk89__87-kbtTGW$DD-L.jpeg'
accent_color: '#08877d'
---


# Processes, Jobs and Scheduling

**Learning Linux - Section 5.12**


### Processes, Jobs and Scheduling 

This section introduces and explains the terms Application, Script, Process, Daemon, Thread and Job. These will be described in more detail in the following sections.

#### Terms covered

- **Application** syn. *Service*
- **Script**
- **Process**
- **Daemon**
- **Threads**
- **Job**

#### *Application*

An **Application** or service is a program, that runs on your machine. Applications are very common and a few examples for **Applications** are:

- NTP
- NFS
- rsyslog
- Apache
- RTRR
- Rsync
- top
- etc.

#### *Script*

A **script** can be a small application or a command, that is written down in a file containing the steps, that the scripts will follow when called. The script includes the algorithm, that explains step by step what the instance calling it has to do in order to execute the script. An example for a script is a shell script, these scripts can be sometimes identified by having the extension *.sh*. 
In the case of a *shell script*, what is written in the script is executed top to bottom, line by line.
An simple example for such a script is the following:

```shell
#!/bin/bash
echo -e " the command 'whoami' returns:\n"
whoami
mkdir -p /home/tklein/script-execution
exedir='/home/tklein/script-execution'
cd ${exedir}
cat /home/tklein/cars_are_best > ${exedir}/cars_are_still_best
echo -e "\nThe file 'cars_are_still_best' has that many lines:"
wc -l ${exedir}/cars_are_still_best
echo -e "^@\nFancy new Line, just sayin'^@\n"
cat ${exedir}/cars_are_still_best | nl
echo -e "^@\nFancy new Line, just sayin'^@\n"
echo 'Script executed successfully, bash out!'

```

Which returns the following output on the command line:

```bash
~ $ bash scripts/real_script.sh
 the command 'whoami' returns:

tklein

The file 'cars_are_still_best' has that many lines and its absolute path is:
5 /home/tklein/script-execution/cars_are_still_best

Fancy new Line, just sayin'

     1  Not just any text file.
     2  The secret car file.
     3  No CAPS, REALLY: This is good stuff.
     4  The faster the car, the quicker it covers distance.
     5  A V12 engine is a twelve-cylinder piston engine. 

Fancy new Line, just sayin'

Script executed successfully, bash out!
~ $ 
```



#### *Process*

An *application* for example generates a *process* with a unique **process id**.

##### Examples for *Process*/*Services* Commands  

- `systemctl` or `service`
  - `systemctl` is the new command on Red Hat 7/8 and replaces `service`
- `ps` lets the user see what *processes* are running on their Linux machine.
- `top` shows the user all *processes* with dependant *processes* and information regarding memory and **CPU** load.
- `kill` stops a *process* by terminating the *process id* or the *process*.
- `crontab` is used to schedule the executions of these *services*, *processes* or *applications* on the system.
  - When one of these is executed, it becomes a *job*.


#### *Daemon*

A *daemon* is a process, that runs continuously in the background. A common use for *daemons* are **updater**. These can for example send a **HTTP**  `GET request` and gets a **HTTP** `response` in return, telling it if there is a new firmware available for download from the server.



#### *Threads*

Every *process* could have multiple *threads* associated with it. A running *application* could have running multiple threads running in the background.

#### *Job*

A *job* or *workorder* runs a *service* or *process* at a scheduled time.

#### `at.`

`at.` is similar to `crontab` as it is used to schedule the execution of  *service*, *process* or *application*, the difference however is that it is only used to do this once. It is not used for reoccurring *jobs*.

