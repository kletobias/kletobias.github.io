---
title: 'Monitoring Users'
subtitle: 'Learning Linux - Section 5.7'
date: 2021-12-28 00:00:00
description: 'This article covers some of the essential commands used in any Linux distribution. Vim text editor was used and CentOS 7 was the OS used in this series. It was setup as command line only virtual machine and accessed through ssh. There are 8 Sections in total.'
featured_image: bash-ga254901e3_1280.png
gallery_images: Bash_GNOME_Terminal_screenshot.png
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

#### *who* command

- Tells one how many people are logged in at the time of running the command.


| Column | Example          |  
|--|-------------------------|  
| uid | kate                 |  
| terminal id for uid |  :0      |  
| time logged in for uid |   2019-03-10 14:33 (:0)     |
| hostname				|	*win11.fritz.box*	|

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

#### *last* command

`last` tells one everything about any user that has logged into the system, ever since the file **/var/log/wtmp** was 
created by default.

```bash
DESCRIPTION
       Last  searches  back through the file /var/log/wtmp (or the file designated by the -f flag) and displays a list of all users logged in (and out) since that file was created.  Names of users and tty's can be given, in which case last will show only those entries matching the arguments.
       Names of ttys can be abbreviated, thus last 0 is the same as last tty0.
```