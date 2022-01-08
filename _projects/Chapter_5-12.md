---
title: 'Processes, Jobs and Scheduling'
subtitle: 'Learning Linux - Section 5.12'
date: 2021-12-07 20:00:00
description: 'This article covers some important commands used for the user account management as often done by system administrators in a corporate environment.'
featured_image: bash-ga254901e3_1280.png
gallery_images: Bash_GNOME_Terminal_screenshot.png
accent_color: '#08877d'
---


### Processes, Jobs and Scheduling 


#### Terms covered

- **Application** syn. Service
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

whoami
echo "${PS1}"
mkdir -p /home/tklein/script-execution
exedir='/home/tklein/script-execution'
cd ${exedir}
cat /home/tklein/cars_are_best > ${exedir}/cars_are_still_best
wc -l ${exedir}/cars_are_still_best
echo -e "^@\nFancy new Line, just sayin'^@\n"
cat ${exedir}/cars_are_still_best
echo -e "^@\nFancy new Line, just sayin'^@\n"
echo 'Script executed successfully, bash out!'
```

Which returns the following output on the command line:

```bash
~ $ bash scripts/real_script.sh # Execution.
tklein

5 /home/tklein/script-execution/cars_are_still_best

Fancy new Line, just sayin'

Not just any text file.
The secret car file.
No CAPS, REALLY: This is good stuff.
The faster the car, the quicker it covers distance.
A V12 engine is a twelve-cylinder piston engine. 

Fancy new Line, just sayin'

Script executed successfully, bash out!
~ $ 
```