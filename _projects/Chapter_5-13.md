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

/Users/tobias/all_code/projects/kletobias-github-io_website/images

{% include post-components/gallery.html
	columns = 1
	full_width = true
	images = "/images/Chapter_5-13-1642816218053.png"
%}


BEST UMANGEE

<img style="width:100%;" id="bright_color_try1.png" src="/images/Chapter_5-13-1642816218053.png"/>

<!---
<img alt="bright_color_try1.png" height="1616" 
src="/images/Chapter_5-13-1642816218053.png" width="2550"/>
-->


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
The commands covered, using the `firewalld` service are the following:

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

The output tells one the following about the status of the service `firewalld`:

- The service is loaded (**LOAD**).
  - That tells one, that the configuration file of the `firewall` service is loaded.
  - From the line above it can be concluded, that `systemctl` can reach and read that configuration file.
  - The configuration file is located at: '/usr/lib/systemd/system/firewalld.service'
- `firewalld` is loaded.
  - A loaded service will start automatically upon any kind of system startup.
- The service is **ACTIVE**.
  - It is currently running.
  - It has been running since *Sun 2022-01-16 16:38:24 CET*
  - Time since start is 5h 54min.
- The manual for `firewalld` can be opened with the command `man firewalld(1)`.
- It has the **PID** 796 (*processid*).
- The control groups (**CGroup**), showing higher level unit hierarchy. This is part of resource management, see [here](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/resource_management_guide/chap-introduction_to_control_groups) for detailed information.
- The last 3 lines give a brief history of the command. It is a log.

###### Example: systemctl stop servicename.service

In this example, the `firewalld` unit is stopped and its status
is checked afterwards, by running `systemctl status firewalld.service`

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


In this example, the `firewalld` unit is started again and its status
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

One can see, that the `firewalld` service is still active, after it has
been disabled. It is still loaded, however it is mentioned in the output, that it is disabled!

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

##### restart & reload

`systemctl restart` and `systemctl reload` are two important commands to
understand.

`systemctl restart` will shut down the specified unit and then immediately
start it back up again. The downtime is minimized. It will also restart a
currently powered off unit, unless the restart statement is replaced by
`try-restart`. This option will only restart a running unit and not a powered
off one.

`systemctl reload` is only supported by some system services and will be ignored
all together by ones that don't support it.
It lets the user change its configuration files and reload the unit to use the
updated configuration files without stopping its service at all. This can be a
great feature for *always online services*, such as web servers.

```bash
systemctl restart servicename.service
systemctl reload servicename.service
```

###### systemctl --all

The `systemctl --all` will list all units in the system's registry.
Here it was used to list all units, so that the one called `mariadb`
would be found using the `grep "maria"` with piped input from
`systemctl --all`.

```bash
root * systemctl --all | grep "maria"
  mariadb.service 
                  active   running   MariaDB database server
root * 
```


###### systemctl restart servicename.service

Restarting the `mariadb` unit like so:

```bash
root * systemctl restart mariadb.service
root * systemctl status mariadb.service
● mariadb.service - MariaDB database server
   Loaded: loaded (/usr/lib/systemd/system/mariadb.service; enabled; vendor preset: disabled)
   Active: active (running) since Tue 2022-01-18 12:10:45 CET; 18s ago
  Process: 24184 ExecStartPost=/usr/libexec/mariadb-wait-ready $MAINPID (code=exited, status=0/SUCCESS)
  Process: 24147 ExecStartPre=/usr/libexec/mariadb-prepare-db-dir %n (code=exited, status=0/SUCCESS)
 Main PID: 24182 (mysqld_safe)
   CGroup: /system.slice/mariadb.service
           ├─24182 /bin/sh /usr/bin/mysqld_safe --basedir=/usr
           └─24347 /usr/libexec/mysqld --basedir=/usr --datadir=/var/lib/mysql --plugin-dir=...

Jan 18 12:10:43 vm8 systemd[1]: Starting MariaDB database server...
Jan 18 12:10:43 vm8 mariadb-prepare-db-dir[24147]: Database MariaDB is probably initialize...e.
Jan 18 12:10:43 vm8 mariadb-prepare-db-dir[24147]: If this is not the case, make sure the ...r.
Jan 18 12:10:43 vm8 mysqld_safe[24182]: 220118 12:10:43 mysqld_safe Logging to '/var/log/...g'.
Jan 18 12:10:43 vm8 mysqld_safe[24182]: 220118 12:10:43 mysqld_safe Starting mysqld daemo...sql
Jan 18 12:10:45 vm8 systemd[1]: Started MariaDB database server.
Hint: Some lines were ellipsized, use -l to show in full.
root * 
```

In the output one can see, that the unit has been running for **18s** only and thus
the restart was successful, since it is up and active again.


###### systemctl reload servicename.service

As mentioned earlier, not all units support the `systemctl reload servicename.service`
command and so is the case for the `mariadb` service, as seen in the following
output:

```bash
root * systemctl reload mariadb.service
Failed to reload mariadb.service: Job type reload is not applicable for unit mariadb.service.
See system logs and 'systemctl status mariadb.service' for details.
root * 
```

A service which supports the `reload` command is the `httpd`
service. One can reload it like so:

```bash
root * systemctl reload httpd.service
```

That is the end for this section.