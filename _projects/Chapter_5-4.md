---
title: 'User Account Management'
subtitle: 'Learning Linux - Section 5.4'
date: 2021-12-29 20:00:00
description: 'This article covers some important commands used for the user account management as often done by system administrators in a corporate environment.'
featured_image: bash-ga254901e3_1280.png
gallery_images: Bash_GNOME_Terminal_screenshot.png
accent_color: '#4ce6b8'
---

### User Account Management

> This article covers some important commands used for the user account management as often done by system administrators in a corporate environment.

#### Commands that will be covered

- `useradd`
- `groupadd`
- `userdel`
- `groupdel`
- `usermod`

#### Important files where user data is stored

- `/etc/passwd`
- `/etc/group`
- `/etc/shadow`

#### Adding a user

##### Example

###### Command

```bash
~ $ Useradd -g superheroes -s /bin/bash -c 'user description' -m -d /home/spiderman spiderman
~ $
```

###### Explanation

From left to right of the command written in the above terminal window\:

- `useradd` is the core command to add an user. The following are all options or arguments of this command. *See `useradd --help` for more details*
  - `-g` defines the group the new user should belong to. Here 'superheroes' is chosen.
  - `-s` defines the shell environment the new user will be using. Shell 'bash' with the executable found in `/bin/bash`
  - `-c` Let\'s one add a user description for the new user in plain text.
  - `-m` defines the user\'s home directory. Here, `/home/spiderman` was chosen.
  - `-d` specifies the name of the user. 'spiderman' in this example.

#### Adding a user in the terminal

- One has to have *root* priviledges in order to do any of the following!
- The user is added by running `useradd <username>`
- To verify, that the user was created, the command `id <username>` is used.
- This command gives additional information, if the username was created correctly /(from left to right in the following)\:
  - `uid=1003(ashley)` **uid** gives the userid and the name of the user the id represents.
  - `gid=1003(ashley)` **gid** gives the group id and name of the group similiar to **uid**. This group will always default to the username. Each user has it\'s own group with the same name, as the user\'s username.
  - `groups=1003(ashley)` **groups** gives the group memberships that the user has. These can but are not limited to other local user groups, like *staff, administrators, it-department* for example.
```bash
~ $ su -
Password:
Last login: Sat Dec 25 19:15:53 CET 2021 on pts/0
root * useradd ashley
root * id ashley
uid=1003(ashley) gid=1003(ashley) groups=1003(ashley)
root *
```

The name of the user that will be created is 'irina'.

##### Adding the user to a group

Creating a new group *superheroes* below.

```bash
root * groupadd superheroes
```
Verifying that the group was created can be done by running the below code. Since the most recently added new group is appended to the bottom of the file */etc/group*, one only has to look at the last line here.

```bash
root * tail -5 /etc/group
tcpdump:x:72:
tklein:x:1000:tklein
irina:x:1001:
ashley:x:1003:
superheroes:x:1004:
root *
```

- Deleting a user is done by using `userdel <username>` and deleting a user and their home directory by use of `userdel -r <username>`.

```bash
root * userdel irina # Only deletes the user, not their home directory
root * cd /home
root * ls -ltr
total 4
drwx------.  2   1001   1002   62 Dec 25 19:24 irina # Home dir still there.
drwx------. 16 tklein tklein 4096 Dec 25 19:48 tklein
drwx------.  2   1002   1002   62 Dec 25 19:53 trish
drwx------.  2 ashley ashley   62 Dec 25 22:36 ashley
root * userdel -r ashley # with `-r` the home dir also gets deleted.
root * ls -ltr
total 4
drwx------.  2   1001   1002   62 Dec 25 19:24 irina
drwx------. 16 tklein tklein 4096 Dec 25 19:48 tklein
drwx------.  2   1002   1002   62 Dec 25 19:53 trish
root *
```

#### Adding \& deleting a group

- The `groupadd <group>` command is used to add a group
- To check whether the group was created, the bottom of */etc/group* can be looked at. The new group has to found at the bottom of the file, assuming it was the most recent addition to the file.

```bash
root * groupadd golfers # Creating group golfers
root * tail -5 /etc/group
stapdev:x:158:
tcpdump:x:72:
tklein:x:1000:tklein
superheroes:x:1004:
golfers:x:1005:
```

- Deleting a group is done with the `groupdel <group name>`
- Verification that the group was deleted is done like in the above example.

```bash
root * groupdel golfers # Delting group golfers
root * tail -5 /etc/group
stapsys:x:157:
stapdev:x:158:
tcpdump:x:72:
tklein:x:1000:tklein
superheroes:x:1004:
root *
```

#### Changing user related information

- Modifying a user account is done with `usermod [options] <login>`


##### `usermod -G  <group name> <username>`

- Adding *username* to another group in addition to their default group.
- In the example below, *brianna* is added to group *golfers*.
- After that it is verified, that the operation was successful.

```bash
root * useradd brianna # Creating user brianna
root * groupadd golfers # Creating group golfers
root * tail -5 /etc/group # Verifying that both were created
superheroes:x:1004:
trish:x:1001:
tyler:x:1002:
brianna:x:1003:
golfers:x:1005:
root * usermod -G golfers brianna # adding brianna to group golfers
root * id brianna # Checking that brianna belongs to both groups now
uid=1003(brianna) gid=1003(brianna) groups=1003(brianna),1005(golfers)
root *
```

- The line `golfers:x:1005:brianna` in the following tells, that brianna is a member of the group golfers. Any other users, that are also a member of this group would be listed in the same row as brianna. Each member\'s username would be separated by a comma. As can be seen in this excerpt\:

```bash
root * useradd veronica
root * usermod -G golfers veronica
root * grep "golfers" /etc/group
golfers:x:1005:brianna,veronica # both users are listed as members.
root *
```

Alternative approaches to the verification\:

- Using `grep "<string>" <file>`

```bash
root * grep "golfers" /etc/group
golfers:x:1005:brianna
root *
```

- Or with `tail [option] <file>`

```bash
golfers:x:1005:brianna
root * tail -5 /etc/group
superheroes:x:1004:
trish:x:1001:
tyler:x:1002:
brianna:x:1003:
golfers:x:1005:brianna
root *
```

