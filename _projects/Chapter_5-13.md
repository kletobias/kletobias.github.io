---
title: 'The systemctl command'
subtitle: 'Learning Linux - Section 5.13'
date: 2022-01-08 00:00:00
description: 'This section is about the systemctl command, as found in CentOS 7. It describes and gives examples of its usage.' 
featured_image: 'mT68055%25%25--tYF_5__5jhhh5pls$0-G.jpeg'
gallery_images: 'YtOk89__87-kbtTGW$DD-L.jpeg'
accent_color: '#08877d'
---


### The *systemctl* command

#### Overview

- The `systemctl` command is a new tool to control system services.
- It is found in CentOS 7 and later.
- `systemctl` command replaces the `service` command.

#### Name, Syntax and Description

From the top of the man page (`man systemctl`), one gets an overview of the name and syntax (*synopsis*) of the `systemctl` command, along with a short description of it.

```man
NAME
       systemctl - Control the systemd system and service manager

SYNOPSIS
       systemctl [OPTIONS...] COMMAND [NAME...]

DESCRIPTION
       systemctl may be used to introspect and control the state of the "systemd" system and service
       manager. Please refer to systemd(1) for an introduction into the basic concepts and
       functionality this tool manages.
```

#### Usage examples

In this section several of the `systemctl` commands are run inside the shell and further explained. The basic syntax used in the examples, referring to the information from the `man systemctl` output from above, is: `systemctl COMMAND [NAME...]`.

```bash
systemctl start servicename.service (firewalld)
systemctl stop servicename.service (firewalld)
systemctl status servicename.service (firewalld)
```


```bash
systemctl enable servicename.service
```

```bash
systemctl restart servicename.service
systemctl reload servicename.service
```