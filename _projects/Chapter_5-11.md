---
title: 'System Utility Commands'
subtitle: 'Learning Linux - Section 5.11'
date: 2022-01-06 07:00:00
description: 'In this Section we look at the difference between some of the popular Directory Services out there. E.g. Active Directory, LDAP, IDM, WinBIND, OpenLDAP.'
featured_image: bash-ga254901e3_1280.png
gallery_images: Bash_GNOME_Terminal_screenshot.png
accent_color: '#08877d'
---

### System Utility Commands

#### Commands covered

- `date`
- `uptime`
- `hostname`
- `uname`
- `which`
- `cal`
- `bc`

#### *date*

The `date` command returns information about the current date of the system. 
It returns the following information from left to right:

| date          |
|---------------|
| Day of the week |
| Month         |
| Day of the month |
| Time          |
| Time zone     |
 | Year				      |

```bash
~ $ date
Tue Dec 28 11:38:47 CET 2021
~ $ 
```


#### *uptime*


| Column No. | Output<br /> Type                                       | Exemplary<br /> Output         |
|------------|---------------------------------------------------------|--------------------------------|
| 1          | Current System Time                                     | 11:37:00                       |
| 2          | Shows for how long the system has been running in total | up 4 days 22:33                |
| 3          | Number of Users currently logged into the Linux system  | 3 users                        |
| 4          | Average **CPU** load for 1, 5 and 15 minute period      | load average: 0.00, 0.01, 0.05 |


```bash
~ $ uptime
 11:52:44 up 4 days, 22:33,  3 users,  load average: 0.00, 0.01, 0.05
~ $ 
```

#### *hostname*

`hostname` tells one about the hostname of the Linux machine one is currently logged in.
`hostname` is used to verify, that one is *actually* logged into the right machine. This can be important to verify before running critical commands on the machine that one is logged in. 

```bash
~ $ hostname
localhost.localdomain
~ $ 
```


