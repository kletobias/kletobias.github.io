---
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


The output, that the `systemctl` command generates is in row form.
Each row shows the values of the variable designated to it. The following
table lists the fields found in the output and describes the values for
each field. The table below was reproduced from the [Red Hat System Administrator's Guide](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html-single/system_administrators_guide/index).


<div class="table" id="tabl-Managing_Services_with_systemd-Services-Status">
    <div class="table-contents">
        <table class="lt-4-cols lt-7-rows">
            <colgroup>
                <col class="col_1" style="width: 50%; "><!--Empty-->
                <col class="col_2" style="width: 50%; "><!--Empty--></colgroup>
            <thead>
            <tr>
                <th align="left" id="idm140499344203312" scope="col" valign="top">Field</th>
                <th align="left" id="idm140499344202224" scope="col" valign="top">Description</th>
            </tr>
            </thead>
            <tbody>
            <tr>
                <td align="left" headers="idm140499344203312" valign="top"><p>
                    <code class="literal">Loaded</code>
                </p>
                </td>
                <td align="left" headers="idm140499344202224" valign="top"><p>
                    Information whether the service unit has been loaded, the absolute path to the unit file, and a note whether the unit is enabled.
                </p>
                </td>
            </tr>
            <tr>
                <td align="left" headers="idm140499344203312" valign="top"><p>
                    <code class="literal">Active</code>
                </p>
                </td>
                <td align="left" headers="idm140499344202224" valign="top"><p>
                    Information whether the service unit is running followed by a time stamp.
                </p>
                </td>
            </tr>
            <tr>
                <td align="left" headers="idm140499344203312" valign="top"><p>
                    <code class="literal">Main PID</code>
                </p>
                </td>
                <td align="left" headers="idm140499344202224" valign="top"><p>
                    The PID of the corresponding system service followed by its name.
                </p>
                </td>
            </tr>
            <tr>
                <td align="left" headers="idm140499344203312" valign="top"><p>
                    <code class="literal">Status</code>
                </p>
                </td>
                <td align="left" headers="idm140499344202224" valign="top"><p>
                    Additional information about the corresponding system service.
                </p>
                </td>
            </tr>
            <tr>
                <td align="left" headers="idm140499344203312" valign="top"><p>
                    <code class="literal">Process</code>
                </p>
                </td>
                <td align="left" headers="idm140499344202224" valign="top"><p>
                    Additional information about related processes.
                </p>
                </td>
            </tr>
            <tr>
                <td align="left" headers="idm140499344203312" valign="top"><p>
                    <code class="literal">CGroup</code>
                </p>
                </td>
                <td align="left" headers="idm140499344202224" valign="top"><p>
                    Additional information about related Control Groups (cgroups).
                </p>
                </td>
            </tr>
            </tbody>
        </table>
    </div>
</div>


#### Usage Examples


In this section several of the `systemctl` commands are run inside the shell and further explained. The basic syntax used in the examples, referring
to the information from the `man systemctl` output from above, is: `systemctl COMMAND [NAME...]`.
The commands covered, using the `firewalld.service` service are the following:

##### start, stop and status

```bash
systemctl start servicename.service (firewalld)
systemctl stop servicename.service (firewalld)
systemctl status servicename.service (firewalld)
```


###### Example: systemctl status servicename.service

The output of the `systemctl status servicename.service`
is explained in detail. The explanation follows the row-wise structure of the output of the command.

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

###### Example: systemctl stop servicename.service

In this example, the `firewalld.service` is stopped and its status
afterwards is checked, by running `systemctl status firewalld.service`

```bash
~ $ su -
Password: 
Last login: Mon Jan 17 13:03:17 CET 2022 on pts/0
root * systemctl stop firewalld.service
root * systemctl status firewalld.service
● firewalld.service - firewalld - dynamic firewall daemon
   Loaded: loaded (/usr/lib/systemd/system/firewalld.service; enabled; vendor preset: enabled)
   Active: inactive (dead) since Tue 2022-01-18 05:10:26 CET; 21s ago
     Docs: man:firewalld(1)
  Process: 23277 ExecStart=/usr/sbin/firewalld --nofork --nopid $FIREWALLD_ARGS (code=exited, status=0/SUCCESS)
 Main PID: 23277 (code=exited, status=0/SUCCESS)

Jan 18 05:10:02 vm8 systemd[1]: Starting firewalld - dynamic firewall daemon...
Jan 18 05:10:02 vm8 systemd[1]: Started firewalld - dynamic firewall daemon.
Jan 18 05:10:02 vm8 firewalld[23277]: WARNING: AllowZoneDrifting is enabled. T...w.
Jan 18 05:10:25 vm8 systemd[1]: Stopping firewalld - dynamic firewall daemon...
Jan 18 05:10:26 vm8 systemd[1]: Stopped firewalld - dynamic firewall daemon.
Hint: Some lines were ellipsized, use -l to show in full.
```


###### Example: systemctl start servicename.service


In this example, the `firewalld.service` is started again and its status
afterwards is checked, by running `systemctl status firewalld.service`
```bash
root * systemctl start firewalld.service
root * systemctl status firewalld.service
● firewalld.service - firewalld - dynamic firewall daemon
   Loaded: loaded (/usr/lib/systemd/system/firewalld.service; enabled; vendor preset: enabled)
   Active: active (running) since Tue 2022-01-18 05:11:30 CET; 3s ago
     Docs: man:firewalld(1)
 Main PID: 23467 (firewalld)
   CGroup: /system.slice/firewalld.service
           └─23467 /usr/bin/python2 -Es /usr/sbin/firewalld --nofork --nopid

Jan 18 05:11:30 vm8 systemd[1]: Starting firewalld - dynamic firewall daemon...
Jan 18 05:11:30 vm8 systemd[1]: Started firewalld - dynamic firewall daemon.
Jan 18 05:11:31 vm8 firewalld[23467]: WARNING: AllowZoneDrifting is enabled. T...w.
Hint: Some lines were ellipsized, use -l to show in full.
root * 
```


##### disable & enable 

While `systemctl stop servicename.service` and  `systemctl start servicename.service`
stop and start a service immediately after execution, the commands
`systemctl disable servicename.service` and `systemctl enable servicename.service`
will do different things compared with `stop` and `start` respectively.

Enable will create hooks for the unit specified in the `systemctl enable...`
command in relevant directories/files, so that the unit will start on boot
automatically or when certain hardware is connected. There is a multitude of possible
triggers one can specify, that will cause the specified unit to start its service.
The trigger has to be specified in the *unit file* of the unit to be enabled.

Similarly, the `systemctl disable...` command will keep a unit from automatically starting,
after a specified trigger or triggers has or have occurred. Enable and disable are like toggles,
a unit can be only enabled or disabled and if currently enabled, it can only be
disabled and vice versa. 

Examples for these two commands follow below.

```bash
systemctl disable servicename.service
systemctl enable servicename.service
```

###### systemctl disable servicename.service

One can see, that the `firewalld` service is still active, after it was
disabled. It is still loaded, however it is mentioned, that it is disabled!

```bash
root * systemctl disable firewalld.service
Removed symlink /etc/systemd/system/multi-user.target.wants/firewalld.service.
Removed symlink /etc/systemd/system/dbus-org.fedoraproject.FirewallD1.service.
root * systemctl status firewalld.service
● firewalld.service - firewalld - dynamic firewall daemon
   Loaded: loaded (/usr/lib/systemd/system/firewalld.service; disabled; vendor preset: enabled)
   Active: active (running) since Tue 2022-01-18 05:11:30 CET; 1h 48min ago
     Docs: man:firewalld(1)
 Main PID: 23467 (firewalld)
   CGroup: /system.slice/firewalld.service
           └─23467 /usr/bin/python2 -Es /usr/sbin/firewalld --nofork --nopid

Jan 18 05:11:30 vm8 systemd[1]: Starting firewalld - dynamic firewall daemon...
Jan 18 05:11:30 vm8 systemd[1]: Started firewalld - dynamic firewall daemon.
Jan 18 05:11:31 vm8 firewalld[23467]: WARNING: AllowZoneDrifting is enabled. T...w.
Hint: Some lines were ellipsized, use -l to show in full.
root * 
```


###### systemctl enable servicename.service

Vice versa, enabling the `firewalld` service again does not change anything in terms of it being loaded and active. However, in the **Loaded** row, one can see that it is now
enabled again.


```bash
root * systemctl enable firewalld.service
Created symlink from /etc/systemd/system/dbus-org.fedoraproject.FirewallD1.service to /usr/lib/systemd/system/firewalld.service.
Created symlink from /etc/systemd/system/multi-user.target.wants/firewalld.service to /usr/lib/systemd/system/firewalld.service.
root * systemctl enable firewalld.service
root * systemctl status firewalld.service
● firewalld.service - firewalld - dynamic firewall daemon
   Loaded: loaded (/usr/lib/systemd/system/firewalld.service; enabled; vendor preset: enabled)
   Active: active (running) since Tue 2022-01-18 05:11:30 CET; 6h ago
     Docs: man:firewalld(1)
 Main PID: 23467 (firewalld)
   CGroup: /system.slice/firewalld.service
           └─23467 /usr/bin/python2 -Es /usr/sbin/firewalld --nofork --nopid

Jan 18 05:11:30 vm8 systemd[1]: Starting firewalld - dynamic firewall daemon...
Jan 18 05:11:30 vm8 systemd[1]: Started firewalld - dynamic firewall daemon.
Jan 18 05:11:31 vm8 firewalld[23467]: WARNING: AllowZoneDrifting is enabled. This is cons...ow.
Hint: Some lines were ellipsized, use -l to show in full.
root * 
```




```bash
systemctl restart servicename.service
systemctl reload servicename.service
```


```bash
systemctl list-units --all
```