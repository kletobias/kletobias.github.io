---
title: 'How to switch users and sudo access'
subtitle: 'Learning Linux - Section 5.6'
date: 2021-12-27 00:00:00
description: 'This article covers some of the essential commands used in any Linux distribution. Vim text editor was used and CentOS 7 was the OS used in this series. It was setup as command line only virtual machine and accessed through ssh. There are 8 Sections in total.'
featured_image: 'mT68055%25%25--tYF_5__5jhhh5pls$0-G.jpeg'
gallery_images: 'jtlkr89487--kbcdtTGWDD-_%$_t.jpeg'
accent_color: '#08877d'
---
### How to switch users and *sudo* access

#### Commands covered

- `su - username`
- `sudo <command>`
- `visudo`

#### Relevant file

- **/etc/sudoers**

#### Routine commands to run after login into a *VM*

Since a virtual machine is used for all the sections and exercises, 
one should make sure that the following values are what they should be.

##### *whoami*: Which user am I?

```bash
~ $ whoami
tklein
~ $ 
```

##### *pwd*: What is my current absolute *path*?

```bash
~ $ pwd
/home/tklein
~ $ 
```

##### *hostname*: On which *host* am I currently?

```bash
~ $ hostname
localhost.localdomain
~ $ 
```

#### *su* and *sudo*

**Command:** `su - username` 

One enters the 'username' of the account one wants to become. If left blank,
it defaults to 'username' == *root*

Becoming user *root* and staying root until one decides to *exit* the root account,
is done like demonstrated below. One must have sufficient permissions to become root and know the password for the 
root user account.

```bash
~ $ su -
Password: 
Last login: Sun Dec 26 23:05:13 CET 2021 on pts/0
root * 
```
While root, one can change into any other *username*, without being prompted to enter that *username's* password.  

```bash
~ $ su -
Password: 
Last login: Mon Dec 27 09:56:48 CET 2021 on pts/0
root * su - kate
[kate@localhost ~]$ 
```

Exiting the root account again is done by entering `exit` after one's prompt.

```bash
root * exit
logout
~ $ whoami
tklein
~ $ 
```

**Command:** `sudo <command>`

The `sudo` command lets a user, who can not become *root* himself. It allows such a user
to run commands, that only user *root* can run usually, if they are in group *wheel* for example or in the **sudoers** file.

Two commands that can only be run by *root* are `dmidecode` and `fdisk -l`, to run these one has to 

```bash
~ $ dmidecode
# dmidecode 3.2
/sys/firmware/dmi/tables/smbios_entry_point: Permission denied
Scanning /dev/mem for entry point.
/dev/mem: Permission denied
~ $ fdisk -l
fdisk: cannot open /dev/sda: Permission denied
fdisk: cannot open /dev/mapper/centos-root: Permission denied
fdisk: cannot open /dev/mapper/centos-swap: Permission denied
~ $ 
```

One can add or change the permissions that a user has, to let them become root for example or
to let them run any command in the shell, if they are a member of group *wheel* by default. This 
group is by default listed in the file `visudo`.

##### Example

The example comes from a file that can be accessed by running `visudo` with *root* privileges.

```bash
## Allow root to run any commands anywhere
root    ALL=(ALL)       ALL
will    ALL=(ALL)       ALL # Only an example
## Allows people in group wheel to run all commands
%wheel  ALL=(ALL)       ALL
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL
```

###### *usermod \-aG* 

Adding account 'tklein' to group *wheel*

```bash
root * usermod -aG wheel tklein
root * 
```

###### Verification

- Using `id <username>` one gets all the groups the user is a member of.
- `grep "wheel" /etc/group` will print a line from the **/etc/group** file, to verify the changes.

```bash
root * id tklein
uid=1000(tklein) gid=1000(tklein) groups=1000(tklein),10(wheel)
root * grep "wheel" /etc/group
wheel:x:10:tklein
root * 
```

##### Retrying dmidecode and fdisk commands

After it was not able to run either `dmidecode` or `fdisk -l` using my user account *tklein*,
now it is possible to run `dmidecode` being part of group wheel:

###### *dmidecode*


```bash
[will@localhost ~]$ su - tklein
Password:
Last login: Mon Dec 27 15:20:49 CET 2021 on pts/1
~ $ whoami
tklein
~ $ sudo dmidecode
[sudo] password for tklein:
# dmidecode 3.2
Getting SMBIOS data from sysfs.
SMBIOS 2.5 present.
10 structures occupying 450 bytes.
Table at 0x3EFFD020.

Handle 0x0000, DMI type 0, 20 bytes
BIOS Information
	Vendor: innotek GmbH
	Version: VirtualBox
	Release Date: 12/01/2006
	Address: 0xE0000
	Runtime Size: 128 kB
	ROM Size: 128 kB
	Characteristics:
		ISA is supported
		PCI is supported
		Boot from CD is supported
		Selectable boot is supported
		8042 keyboard services are supported (int 9h)
		CGA/mono video services are supported (int 10h)
		ACPI is supported
		UEFI is supported
Handle 0x0001, DMI type 1, 27 bytes
Handle 0x0001, DMI type 1, 27 bytes
System Information
	Manufacturer: innotek GmbH
	Product Name: VirtualBox
	Version: 1.2
	Serial Number: 0
	UUID: 008f59e3-ffb4-5947-aaba-763e1257b612
	Wake-up Type: Power Switch
	SKU Number: Not Specified
	Family: Virtual Machine
Handle 0x0008, DMI type 2, 15 bytes

...
```

###### The *fdisk \-l* command:

```bash
~ $ sudo fdisk -l
WARNING: fdisk GPT support is currently new, and therefore in an experimental phase. Use at your own discretion.

Disk /dev/sda: 10.7 GB, 10737418240 bytes, 20971520 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk label type: gpt
Disk identifier: 8C3022AF-D83D-4714-A904-26629F38B595


#         Start          End    Size  Type            Name
 1         2048       411647    200M  EFI System      EFI System Partition
 2       411648      2508799      1G  Microsoft basic
 3      2508800     20969471    8.8G  Linux LVM

Disk /dev/mapper/centos-root: 8376 MB, 8376025088 bytes, 16359424 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes


Disk /dev/mapper/centos-swap: 1073 MB, 1073741824 bytes, 2097152 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes

~ $
```

