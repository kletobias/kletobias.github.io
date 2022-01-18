---
It can be downloaded from the internet for free.
title: 'The systemctl command' 
subtitle: 'Learning Linux - Section 5.13'
date: 2022-01-08 00:00:00
description: 'This section is about the systemctl command, as found in CentOS 7. It describes and gives examples of its usage.'
featured_image: 'mT68055%25%25--tYF_5__5jhhh5pls$0-G.jpeg'
gallery_images: 'YtOk89__87-kbtTGW$DD-L.jpeg' 
accent_color: '#08877d'
---


### The *systemctl* Command


#### Overview


- The `systemctl` command is a new tool to control system services.
- It is found in CentOS 7 and later.
- `systemctl` command replaces the `service` command.


#### Name, Syntax and Description


From the top of the man page (`man systemctl`), one gets an overview of the name and syntax (*synopsis*) of the `systemctl` command, along with a
short description of it.


```
systemctl - Control the systemd system and service manager

SYNOPSIS
systemctl [OPTIONS...] COMMAND [NAME...]

DESCRIPTION
systemctl may be used to introspect and control the state of the
"systemd" system and service manager. Please refer to systemd(1)
for an introduction into the basic concepts and functionality
this tool manages.
```


#### *systemctl* Output


The output, that the `systemctl` command generates is in column form. Each column shows the values of the variable designated to it. The following
table lists the columns found in the output and describes the values for each column.


| Column                                                                                         | Description                                                                                                           |
|:----------------------------------------------------------------------------------------------:|:----------------------------------------------------------------------------------------------------------------------|
| **UNIT**                                                                                       | The `systemd` unit name.                                                                                              |
| **LOAD**                                                                                       | Whether the unit's configuration has been parsed by `systemd`.<br />The configuration of loaded units is kept in memory. |                                                                                            |                                                                                                                          |
| **ACTIVE**                                                                                     | A brief summary of whether the unit is active.                                                                        |
| **SUB**                                                                                        | This is a lower level state that gives more detailed information about the unit than **ACTIVE** does. This often varies by type, state and the actual method in which the unit runs.                                 |
| **DESCRIPTION**                                                                                | A short text description about a unit, mentioning purpose and way of operation of it.                                 |


#### Usage Examples


In this section several of the `systemctl` commands are run inside the shell and further explained. The basic syntax used in the examples, referring
to the information from the `man systemctl` output from above, is: `systemctl COMMAND [NAME...]`.


```bash
systemctl start servicename.service (firewalld)
systemctl stop servicename.service (firewalld)
systemctl status servicename.service (firewalld)
```

```bash
~ $ su -
Password: 
systemctl status firewalld.service
● firewalld.service - firewalld - dynamic firewall daemon
   Loaded: loaded (/usr/lib/systemd/system/firewalld.service; enabled; vendor preset: enabled)
   Active: active (running) since Sun 2022-01-16 16:38:24 CET; 5h 54min ago
     Docs: man:firewalld(1)
 Main PID: 796 (firewalld)
   CGroup: /system.slice/firewalld.service
           └─796 /usr/bin/python2 -Es /usr/sbin/firewalld --nofork --nopid

Jan 16 16:38:23 192.168.178.196 systemd[1]: Starting firewalld - dynamic firewall daemon...
Jan 16 16:38:24 192.168.178.196 systemd[1]: Started firewalld - dynamic firewall daemon.
Jan 16 16:38:25 192.168.178.196 firewalld[796]: WARNING: AllowZoneDrifting is enabled. This is considered an insecur... now.
Hint: Some lines were ellipsized, use -l to show in full.
root * 
```

The output tells one the following about the status of the service `firewalld.service`:

- The service is loaded (**LOAD**).
  - That tells one, that the configuration file of the `firewall.service` service is loaded.
  - From the line above it can be concluded, that `systemctl` can reach and read that configuration file.
  - The configuration file is located at: '/usr/lib/systemd/system/firewalld.service'
- `firewalld.service` is loaded.
  - A loaded service will start automatically upon any kind of system startup.
- The service is **ACTIVE**.
  - It is currently running.
  - It has been running since *Sun 2022-01-16 16:38:24 CET*
  - Time since start is 5h 54min.
- The manual for `firewalld.service` can be opened with the command `man firewalld(1)`.
- It has the **PID** 796 (*processid*).
- The control groups (**CGroup**), showing higher level unit hierarchy. This is part of resource management, see [here](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/resource_management_guide/chap-introduction_to_control_groups) for detailed information.
- The last 3 lines give a brief history of the command. It is a log.

```bash
systemctl enable servicename.service
```


```bash
systemctl restart servicename.service
systemctl reload servicename.service
```


```bash
systemctl list-units --all
```