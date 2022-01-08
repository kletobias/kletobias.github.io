---
title: 'Monitoring Users'
subtitle: 'Learning Linux - Section 5.7'
date: 2021-12-28 00:00:00
description: 'This article covers some of the essential commands used in any Linux distribution. Vim text editor was used and CentOS 7 was the OS used in this series. It was setup as command line only virtual machine and accessed through ssh. There are 8 Sections in total.'
featured_image: 'enegative-space-abstract-grunge-swirl-texture.jpeg'
gallery_images: 'enegative-space-rusty-metals-paint-flakes.jpeg'
accent_color: '#08877d'
---

### How to monitor users

#### Commands covered

- `who`
- `last`
- `w`
- `finger`
- `id`

#### Routine commands after login

After having logged in into the virtual machine, one runs, as always, the following commands:

```bash
Last login: Mon Dec 27 15:21:26 2021
~ $ whoami
tklein
~ $ pwd
/home/tklein
~ $ hostname
localhost.localdomain
~ $ 
```

#### *who*

- Tells one how many people are logged in at the time of running the command.


| Column | Example          |  
|--------|-------------------|  
| **Username** | kate                 |  
| **Terminal id for uid** |  :0      |  
| **Time logged in for uid** |   2019-03-10 14:33 (:0)     |
| **Hostname**				|	*win11.fritz.box*	|

```bash
~ $ who
tklein   tty1         2021-12-23 13:19
tklein   pts/0        2021-12-27 17:16 (win11.fritz.box)
tklein   pts/1        2021-12-27 15:20 (win11.fritz.box)
kate     pts/2        2021-12-27 18:16 (win11.fritz.box)
will     pts/3        2021-12-27 18:17 (win11.fritz.box)
~ $ 
```

`who` is oftentimes used, if the system is running slow and the system administrator wants to check who is logged in and how many are 
logged in.

#### *last*

`last` tells one everything about any user that has logged into the system, ever since the file **/var/log/wtmp** was 
created, by default.

```bash
DESCRIPTION
       Last  searches  back through the file /var/log/wtmp (or the file designated by the -f flag) and displays a list 
       of all users logged in (and out) since that file was created.  Names of users and tty's can be given, in which 
       case last will show only those entries matching the arguments.
       Names of ttys can be abbreviated, thus last 0 is the same as last tty0.
```

##### Sample output from running *last*

```bash
~ $ last | more
# User	 Terminal	 Hostname  	Most recent login  Time of logout + Time was onlline.
will     pts/3        imac2017.fritz.b Mon Dec 27 18:17   still logged in   
kate     pts/2        imac2017.fritz.b Mon Dec 27 18:16   still logged in   
tklein   pts/0        imac2017.fritz.b Mon Dec 27 17:16   still logged in   
tklein   pts/1        imac2017.fritz.b Mon Dec 27 15:20   still logged in   
tklein   pts/0        imac2017.fritz.b Mon Dec 27 08:53 - 16:53  (07:59)    
tklein   pts/0        imac2017.fritz.b Sun Dec 26 23:03 - 00:16  (01:12)    
tklein   pts/0        imac2017.fritz.b Sun Dec 26 15:21 - 17:48  (02:26)    
tklein   pts/1        imac2017.fritz.b Sun Dec 26 08:19 - 22:58  (14:38)    
tklein   pts/0        tobiass-imac.fri Sat Dec 25 12:37 - 09:49  (21:11)    
tklein   pts/0        tobiass-imac.fri Sat Dec 25 04:02 - 12:31  (08:28)    
tklein   pts/2        tobiass-imac.fri Sat Dec 25 02:37 - 04:38  (02:00)    
tklein   pts/1        192.168.178.101  Fri Dec 24 23:50 - 03:15  (03:25)    
tklein   pts/0        tobiass-imac.fri Fri Dec 24 23:49 - 03:15  (03:26)    
tklein   pts/0        tobiass-imac.fri Fri Dec 24 22:49 - 23:47  (00:58)    
tklein   pts/0        tobiass-imac.fri Fri Dec 24 20:34 - 22:48  (02:13)    
tklein   pts/0        tobiass-imac.fri Fri Dec 24 17:35 - 20:34  (02:58)    
tklein   pts/0        tobiass-imac.fri Fri Dec 24 16:54 - 17:17  (00:23)    
tklein   pts/1        tobiass-imac.fri Fri Dec 24 05:06 - 16:51  (11:45)    
tklein   pts/0        tobiass-imac.fri Fri Dec 24 02:10 - 05:27  (03:17)    
tklein   pts/0        tobiass-imac.fri Thu Dec 23 13:20 - 02:08  (12:47)    
tklein   tty1                          Thu Dec 23 13:19   still logged in   
reboot   system boot  3.10.0-1160.el7. Thu Dec 23 13:19 - 21:20 (4+08:01)   
tklein   tty1                          Thu Dec 23 13:17 - 13:19  (00:01)    
reboot   system boot  3.10.0-1160.el7. Thu Dec 23 13:17 - 21:20 (4+08:03)   

wtmp begins Thu Dec 23 13:17:01 2021
~ $ 
```

| Column No. 	| Description                                	     |             Example            	|
|:----------:	|--------------------------------------------------|:------------------------------:	|
|      1     	| **Username**                                   	 |              will              	|
|      2     	| **Terminal id**                                	 |              PTS/1             	|
|      3     	| **User's IP Address / Hostname**               	 |     169.254.245.11 / myvm1     	|
|      4     	| **Most Recent Login**                          	 |        Mon Dec 27 17:16        	|
|      5     	| **Most Recent Logout**                         	 | - 16:53 or '*still logged in*' 	|
|      6     	| **Timespan user was online most recently** 	     |         (07:59) (hh:mm)        	|

The following example shows how one can get column 1 alone printed in the console, have its values sorted and filter 
the unique values of column 1. The final pipe of the output will have the output printed with the line numbers for each unique 
entry of column 1.

*Note: awk only works in column 1 here. It separates columns by whitespace by default and the output of `last` is inconsistent 
in its column separation. Whitespace can be found in most of the values in its columns and so, one might have to add a different 
separator with the help of regular expressions to make this a CSV like table. It even prints wtmp at the bottom, because 
it aligns with the first column of the output.*

```bash
~ $ last | awk '{print $1}' | sort | uniq | nl
       
     1  kate
     2  reboot
     3  tklein
     4  will
     5  wtmp # Not part of the first column.
~ $ 
```

#### The *w*

The `w` command gives a similar output to the one `less` generates, but it gives more information, 
more detail compared to the latter.

##### Syntax for the *w* command

`w [OPTIONS] [USER]`  

##### The fields of the *w* table output

The fields found in the output of `w` are listed and described. An example for the values one can find in the output is given as well.

| Column     | Description                                                                                | Example         |
|------------|--------------------------------------------------------------------------------------------|-----------------|
| **USER**  | Prints the username                                                                        | *kate*          |
| **TTY**    | Name of the terminal used by the user                                                      | tty1            |
| **FROM**   | The hostname or IP from where the user is logged in                                        | 169.117.128.105 |
| **LOGIN@** | The time when the user logged in                                                           | 8:30            |
| **IDLE**   | The time since the user last interacted with the terminal,<br /> idle time                 | 7:19m           |
| **JCPU**   | The time used by all the processes attached to the tty                                     | 0.04s           |
| **PCPU**   | The time used by the user's current process.<br /> The one displayed in the **WHAT** field | 0.04s           |
| **WHAT**   | The user's current process and options/arguments                                           | w               |


##### *w* with no options or arguments

`w`

```bash
~ $ w
 23:01:40 up 4 days,  9:42,  5 users,  load average: 0.00, 0.01, 0.05
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
tklein   tty1                      Thu13    2days  0.04s  0.04s -bash
tklein   pts/0    imac2017.fritz.b 17:16    4.00s  0.07s  0.02s w
tklein   pts/1    imac2017.fritz.b 15:20    7:19m  0.08s  0.02s -bash
kate     pts/2    imac2017.fritz.b 18:16    4:45m  0.03s  0.03s -bash
will     pts/3    imac2017.fritz.b 18:17    4:44m  0.03s  0.03s -bash
~ $ 
```
###### *w* with the \[USER\] argument

`w tklein`

```bash
~ $ w tklein
 23:59:05 up 4 days, 10:39,  5 users,  load average: 0.00, 0.01, 0.05
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
tklein   tty1                      Thu13    2days  0.04s  0.04s -bash
tklein   pts/0    imac2017.fritz.b 17:16    1.00s  0.05s  0.00s w tklein
tklein   pts/1    imac2017.fritz.b 15:20    8:16m  0.08s  0.02s -bash
~ $ 
```


#### *finger*

`finger` is not part of the packages that come with a default **CentOS 7.9** installation.<br />
However it is a very powerful tool to have in one's arsenal when it comes to user monitoring. 
It can be installed easily, if one has *root privileges*.<br />
It can be installed using package manager **yum** like so:<br />
`yum install finger -y`

Somehow `finger` took the descriptions I added for users *kate* and *will* and just split them<br />
over the columns **Name** and **Office**. I added the descriptions to the `useradd` command. <br />
`useradd ... -c "User is a real cyclist, no ebike.`<br />
Looking up `man useradd` the answer is quickly found. `-c` is *currently* used as the field for the user's full name.<br />
That is what it says.

>        -c, --comment COMMENT
>           Any text string. It is generally a short description of the login,
>			and is currently used as the field for the user's full name.


```bash
~ $ finger
Login    Name                    Tty      Idle  Login Time   Office     Office Phone   Host
kate     User is a real cyclist  pts/2    6:38  Dec 27 18:16  no ebike.                (imac2017.fritz.box)
tklein   tklein                  tty1       2d  Dec 23 13:19           
tklein   tklein                  pts/0          Dec 27 17:16                           (imac2017.fritz.box)
tklein   tklein                  pts/1    9:12  Dec 27 15:20                           (imac2017.fritz.box)
will     His wife says           pts/3    6:37  Dec 27 18:17  that his                 (imac2017.fritz.box)
~ $ 
```

#### *id*

##### Syntax of the command

`id [username]`

The `id` command can be entered without any further arguments. Like that it will print information  
of the user that runs the command in the shell. See first line of the example for that.  
It will always display:
-The *uid*, the numerical, unique key that every user has. It is between **UID_MIN** and **UID_MAX**, as covered in 5.5.
- The *gid* is the numerical, unique representation of the **group**, that a user is a member of. Something like a user group.
- *groups* lists further groups and group ids of groups that the user is a member of.

```bash
~ $ id
uid=1000(tklein) gid=1000(tklein) groups=1000(tklein),10(wheel) context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
~ $ id will
uid=1005(will) gid=1005(golfers) groups=1005(golfers)
~ $ id kate
uid=1006(kate) gid=1007(cyclists) groups=1007(cyclists)
~ $ 
```
