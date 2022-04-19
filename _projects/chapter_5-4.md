---
title: 'Learning Linux - Chapter 5: Section 4'
description: 'In Chapter 5 Section 4, we take a look at some important commands used for the user account management, as often done by system administrators in a corporate environment.'
date: 2022-01-01 05:04:00
featured_image: 'mT68055%25%25--tYF_5__5jhhh5pls$0-G.jpeg'
gallery_images: 'YtOk89__87-kbtTGW$DD-L.jpeg'
accent_color: '#08877d'
---



# User Account Management

**Learning Linux - Section 5.4**

This article covers some important commands used for the user account management, as often done by system administrators in a corporate environment.

#### Commands that will be covered

- `useradd`
- `groupadd`
- `userdel`
- `groupdel`
- `usermod [-G]`

#### Important files where user data is stored

- **/etc/passwd**
- **/etc/group**
- **/etc/shadow**

#### Adding a user

##### Example

###### Command

```bash
~ $ Useradd -g superheroes -s /bin/bash -c 'user description' -m -d /home/spiderman spiderman
~ $
```

###### Explanation

From left to right of the command written in the above terminal window\:

- `useradd` is the core command to add a user. The following are all options or arguments of this command. *See `useradd --help` for more details*
  - `-g` defines the group the new user should belong to. Here 'superheroes' is chosen.
  - `-s` defines the shell environment the new user will be using. Shell 'bash' with the executable found in **/bin/bash**
  - `-c` Let\'s one add a user description for the new user in plain text.
  - `-m` defines the user\'s home directory. Here, **/home/spiderman** was chosen.
  - `-d` specifies the name of the user. 'spiderman' in this example.

#### Adding a user in the terminal

- One has to have `root` privileges in order to do any of the following!
- The user is added by running `useradd <username>`
- To verify, that the user was created, the command `id <username>` is used.
- This command gives additional information, if the username was created correctly (from left to right in the following)\:
  - `uid=1003(ashley)` **uid** gives the userid and the name of the user the id represents.
  - `gid=1003(ashley)` **gid** gives the group id and name of the group similar to **uid**. This group will always default to the username. Each user has it\'s own group with the same name, as the user\'s username.
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
superheroes:x:1004: # The group 'superheroes' was created
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

#### Adding & deleting a group

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
root * groupdel golfers # Deleting group golfers
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


##### `usermod -G  \<group name> \<username>`

- Adding `username` to another group in addition to their default group.
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

#### Adding a user to another group in the `/home` directory

- Using `usermod -G` to change the group memberships of a user does not change the group that is displayed in the **/home** directory.
- Example of this behavior can be seen in the following example for the user *veronica*. She was added to group *golfers*, but still her group *veronica* is shown below.

```bash
root * ls -ltr
total 4
drwx------. 16 tklein   tklein   4096 Dec 25 19:48 tklein
drwx------.  2 tyler    tyler      62 Dec 26 02:30 tyler
drwx------.  2 brianna  brianna    62 Dec 26 02:31 brianna
# Still group veronica is shown below
drwx------.  2 veronica veronica   62 Dec 26 02:44 veronica
root *
```


```bash
root * chgrp -R golfers veronica
root * ls -ltr
total 4
drwx------. 16 tklein   tklein  4096 Dec 25 19:48 tklein
drwx------.  2 tyler    tyler     62 Dec 26 02:30 tyler
drwx------.  2 brianna  brianna   62 Dec 26 02:31 brianna
# Now group has changed to golfers for veronica
drwx------.  2 veronica golfers   62 Dec 26 02:44 veronica
root *
```

#### Making sense of the structure of file `/etc/passwd`

- The `Password` column only tells, if a password is set for the user. It will display an 'x', if one is stored in the `/etc/shadow` file.
- `uid` is the user id.
- `gid` is the group id.
- `Description` can be added as an option when using the `useradd` command, it is option `useradd ... -c 'description of this user.' ...`
- *Home Directory* gives the path equivalent to `echo $HOME` for the user.
- *Shell of User* gives the name of the user\'s shell environment, as well as the path to the executable of that shell.
  - For CentOS 7, available shells are\:

```bash
root * cat /etc/shells
/bin/sh
/bin/bash
/usr/bin/sh
/usr/bin/bash
/bin/tcsh
/bin/csh
root *
```

**Table 1\:** The 7 columns found in the '.csv' like structure inside the */etc/passwd* file are described and assigned to the columns.

| Column No. |         Variable          |
|:----------:|:-------------------------:|
|  Column 1  |         Username          |
|  Column 2  |         Password          |
|  Column 3  |            uid            |
|  Column 4  |            gid            |
|  Column 5  |        Description        |
|  Column 6  |      Home Directory       |
|  Column 7  | Shell Environment of User |


##### Sample output of `/etc/passwd`

```bash
brianna:x:1003:1003::/home/brianna:/bin/bash
veronica:x:1004:1006::/home/veronica:/bin/bash
root *
```

#### Making sense of the structure of file `/etc/group`

- *Group Password* is the same for every member in the group.
- *Members of the group* lists all members of the group, separated by ','

| Column 1  |      Group Name      |
|-----------|:--------------------:|
 | Column 2  |    Group Password    |
 | Column 3  |         gid          |
 | Column 4  | Members of the group |


#### Making sense of the structure of file `/etc/shadow`

1. `Username` is the login name of the user.
2. `Password` is the user\'s encrypted password.
   - It should contain a minimum of 8-12 characters.
   - Include special characters, like digits, lower and upper case alphabetic characters and other ones as well.
   - Usually the password format is set to `$id$salt$hashed`.
   - The `$id` is the algorithm used on GNU/Linux as follows\:
     1. `$1$` is MD5
     2. `$2a$` is Blowfish
     3. `$2y$` is Blowfish
     4. `$5$` is SHA-256
     5. `$6$` is SHA-512
3. `Last password change`\: Days since the date 01/01/1970 that password was last changed.
4. `Minimum`\: The minimum number of days required between password changes.
		  - E.g. The number of days left before the user is allowed to change his password.
5. `Maximum`\: The maximum number of days, that the password is still valid. The user will have to change their password after that period is over.
6. `Warn`\: Threshold for the number of days in column 5, when a warning is sent to the user that they must change their password soon.
7. `Inactive`\: The number of days, that an account is still active after the `Maximum` has reached 0. It will become inactive after that period has passed without a password change.
8. `Expire`\: Days increase from the specific date 01/01/1970, where the account can no longer be used anymore. It depends on the value set for `Expire`.


| Column 1 | Username      |
|----------|---------------|
| Column 2 | Password      |
| Column 3 | 'lastchanged' |
| Column 4 | Minimum       |
| Column 5 | Maximum       |
| Column 6 | Warn          |
| Column 7 | Inactive      |
| Column 8 | Expire        |

##### Looking up information for a specific user

Information about a user can be gained by running `grep "<username>" /etc/group|/etc/passwd|/etc/shadow` or all three at once:

###### Bash Example

```bash
root * grep "veronica"  /etc/group /etc/passwd /etc/shadow
/etc/group:golfers:x:1005:brianna,veronica
/etc/group:veronica:x:1006:
/etc/passwd:veronica:x:1004:1006::/home/veronica:/bin/bash
/etc/shadow:veronica:!!:18987:0:99999:7:::
root *
```

#### Final Example

Creating a new user and adding them to a group, specifying their shell environment, adding a description, setting their home directory and their username can all be done in one long command like so\:

```bash
root * useradd -g golfers -s /bin/bash -c "His wife says, that his handicap is rubbish." -m -d /home/will will
root * ls -ltr /home/
total 4
drwx------. 16 tklein   tklein  4096 Dec 25 19:48 tklein
drwx------.  2 tyler    tyler     62 Dec 26 02:30 tyler
drwx------.  2 brianna  brianna   62 Dec 26 02:31 brianna
drwx------.  2 veronica golfers   62 Dec 26 02:44 veronica
drwx------.  2 will     golfers   62 Dec 26 08:34 will # will is a member of group golfers.
root * grep "will" /etc/group /etc/passwd /etc/shadow
/etc/passwd:will:x:1005:1005:His wife says, that his handicap is rubbish.:/home/will:/bin/bash
/etc/shadow:will:!!:18987:0:99999:7:::
```

##### Creating the password for user 'will'

```bash
root * passwd will
Changing password for user will.
New password:
Retype new password:
passwd: all authentication tokens updated successfully.
root *
```

