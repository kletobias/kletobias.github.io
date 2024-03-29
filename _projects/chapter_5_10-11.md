---
title: 'Learning Linux - Chapter 5: Section 10 & 11'
description: 'Sections 10 and 11 describe popular directory services and system utility commands.'
date: 2022-01-01 05:10:11
featured_image: 'mT68055%25%25--tYF_5__5jhhh5pls$0-G.jpeg'
gallery_images: 'YtOk89__87-kbtTGW$DD-L.jpeg'
accent_color: '#08877d'
---



# Overview and Comparison of Popular Directory Services

**Learning Linux - Section 5.10**



### Overview and Difference between Popular Directory Services

- Linux is mostly used in corporate environments, by developers and system administrators for example. One of the main reasons Linux is chosen in these scenarios, is its safety and performance it has over Windows for example. The user base is limited.
- Windows has a product called *Active Directory* for account authentication.
  - For example, facebook runs on Linux behind the scenes. However, a Windows user will not log into a Linux client when they log in, in their browser.
  - There a middle man is used, that handles the login process that is some kind of *Directory Service*.
- *IDM* = Identity Manager
  - Red Hat built this product for companies that have many Linux users, in order to deal with the great number of employees that have to log in for one service or another.
  - It runs on Linux and is used for large corporate environments.
- *WinBIND* = Used in Linux to communicate with Windows (Samba).
  - Samba came up with this 'addon', that lets Linux users authenticate themselves against Windows *Active Directory*.
  - Use case is also Widows *Active Directory* users, that have to authenticate against a Linux server.
- *OpenLDAP* (open source)
  - It is an open source alternative to *IDM* developed by Red Hat. *IDM* is shareware, while *OpenLDAP* is free.
- *IBM Directory Server*
  - Proprietary technology, developed by IBM.
- *JumpCloud*
  - Another directory service option.
- *LDAP* = Lightweight Directory Access Protocol
  - *LDAP* is a protocol and not a service.
  - It is needed to communicate to any *Directory Service* 

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

# System Utility Commands

**Learning Linux - Section 5.11**




### Commands covered

- `date`
- `uptime`
- `hostname`
- `uname`
- `which`
- `cal`
- `bc`

#### `date`

The `date` command returns information about the current date of the system. 
It returns the following information from left to right:


| Column No. | date             |
|:----------:|------------------|
| 1          | Day of the week  |
| 2          | Month            |
| 3          | Day of the month |
| 4          | Time             |
| 5          | Time zone        |
 | 6          | Year             |


```bash
~ $ date
Tue Dec 28 11:38:47 CET 2021
~ $ 
```


#### `uptime`

The `uptime` command gives information about the system. Namely about for how long it has been running in total, the number of currently online users and the **CPU** load. The **CPU** load is measured by looking at the average number of jobs in the system's *run queue* for 3 different time periods. The periods are 1, 5 and 15 minutes.


| Column No. | Data                                                    | Example                        |
|:----------:|---------------------------------------------------------|--------------------------------|
| 1          | Current System Time                                     | 11:37:00                       |
| 2          | Shows for how long the system has been running in total | up 4 days 22:33                |
| 3          | Number of Users currently logged into the Linux system  | 3 users                        |
| 4          | Average **CPU** load for 1, 5 and 15 minute period      | load average: 0.00, 0.01, 0.05 |


```bash
~ $ uptime
 11:52:44 up 4 days, 22:33,  3 users,  load average: 0.00, 0.01, 0.05
~ $ 
```

#### `hostname`

`hostname` tells one about the hostname of the Linux machine one is currently logged in.
`hostname` is used to verify, that one is *actually* logged into the right machine. This can be important to verify before running critical commands on the machine that one is logged in. 

```bash
~ $ hostname
localhost.localdomain
~ $ 
```


#### `uname`

`uname` gives very brief information about the operating system, that is running on the current machine.

##### Example


```bash
~ $ uname
Linux
~ $ 
```


###### `uname -a`


With the option `-a` one gets more information. In addition to the type of operating system (*Linux*), it prints more details 
about the operating system as one can see in the example below.


###### Example


```bash
~ $ uname -a
Linux localhost.localdomain 3.10.0-1160.el7.x86_64 #1 SMP Mon Oct 19 16:18:59 UTC 2020 x86_64 x86_64 x86_64 GNU/Linux
~ $ 
```


#### `which`

The structure of the command is `which [options] [--] programname [...]` and it tells one, as stated in the man pages of `which`:

> which - shows the full path of (shell) commands.

The command can be used for example with the following types of commands: `which [command]` `which [alias]` or `which [variable]`.

##### Example


```bash
~ $ which pwd
/usr/bin/pwd

~ $ which $HOME
/usr/bin/which: no tklein in (/home)

~ $ which vi
alias vi='vim'
        /usr/bin/vim
~ $ 
```


#### `cal`

From the man pages of `cal`, one learns that the syntax of the command looks like this: `cal [options] [[[day] month] year]`

`cal` simply prints a calendar, that looks like in the example below. It will take the system date as the current date.

##### Example

The tool is mainly intended to be used as a quick way to view a calendar in the terminal.


```bash
~ $ cal
    December 2021   
Su Mo Tu We Th Fr Sa
          1  2  3  4
 5  6  7  8  9 10 11
12 13 14 15 16 17 18
19 20 21 22 23 24 25
26 27 28 29 30 31

~ $ 
```


#### `bc`

`bc` = Binary calculator
It is a basic calculator, that lacks builtin functions like *factorial (n!)* or any `root` function. These functions can however be defined in a separate text file and can be imported like that over and over again.


```bash
~ $ bc
bc 1.06.95
Copyright 1991-1994, 1997, 1998, 2000, 2004, 2006 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type `warranty'. 
2^10
1024
5*10^6/120
41666
```

