---
title: chage command in depth
subtitle: 'Learning Linux - Section 5.5'
date: 2021-11-30 05:05:00
description: 'The /etc/login.defs File is described and the use of the variables that are defined inside this file in terms of their role during the usage of useradd command.'
featured_image: bash-ga254901e3_1280.png
gallery_images: Bash_GNOME_Terminal_screenshot.png
accent_color: '#08877d'
---

### *chage* command in depth

`chage` = 'change age' 

The command has the following important options. It is a command that is designed to be used for an individual user,
in the way it is shown here. In a corporate environment much this is automated, so one does not have to define values for each user that has to be created. Default values are used instead.


| Option | Description     | Example                                                                                      |
|:------:|-----------------|----------------------------------------------------------------------------------------------|
| `-m`   | MIN DAYS        | Minimum days between password changes                                                        |
| `-M`   | MAX DAYS        | Maximum period, before user is forced to change his/her password                             |
| `-d`   | LAST DAY        | The number of days, counting from 01/01/1970, where the most recent password change happened |
| `-I`   | INACTIVE        | The number of days, after the password expires, that a account gets disabled                 |
| `-E`   | EXPIRATION DATE | Number of days starting from 01/01/1970, where the account will be disabled                  |
| `-W`   | PASS_WARN_AGE   | The number of days before a user's password expires, that a warning is given to him          |
| `User` | USERNAME        | The username                                                                                 |


#### Source of the default values

- The file used to save the default values is **/etc/login.defs**.
  - The terms defined in the file are the following (running a quick `egrep` search, as shown below).
  - The values for the terms in this file are the ones used, when one creates a user by running the command `useradd`.


```bash
root * egrep "^[A-Z\_]+" /etc/login.defs 
MAIL_DIR        /var/spool/mail
PASS_MAX_DAYS   99999
PASS_MIN_DAYS   0
PASS_MIN_LEN    5
PASS_WARN_AGE   7
UID_MIN         1000
UID_MAX         60000
SYS_UID_MIN     201
SYS_UID_MAX     999
GID_MIN         1000
GID_MAX         60000
SYS_GID_MIN     201
SYS_GID_MAX     999
CREATE_HOME     yes
UMASK           077
USERGROUPS_ENAB yes
ENCRYPT_METHOD  SHA512
root * 
```

| Variable        |     Example	      |                                          Description                                          |
|-----------------|:-----------------:|:---------------------------------------------------------------------------------------------:|
| MAIL_DIR        | /var/spool/mail 	 |                          The absolute path to user's mail directory                           |
| PASS_MAX_DAYS   | 99999           	 |             Sets the maximum number of days the user has to change their password             |
| PASS_MIN_DAYS   | 0               	 | The user has to wait the here defined number of days, before he/she can change their password |
| PASS_MIN_LEN    | 5               	 |                      The minimum length, that a user password must have.                      |
| PASS_WARN_AGE   | 7               	 |    The number of days before a users's password expires, that a warning is given to him.     |
| UID_MIN         | 1000            	 |                                    The lower limit for uid                                    |
| UID_MAX         | 60000           	 |                                    The upper limit for uid                                    |
| SYS_UID_MIN     | 201             	 |                              UID_MIN for 'system process users'                               |
| SYS_UID_MAX     | 999             	 |                              UID_MAX for 'system process users'                               |
| GID_MIN         | 1000            	 |                                    The lower limit for gid                                    |
| GID_MAX         | 60000           	 |                                    The upper limit for gid                                    |
| SYS_GID_MIN     | 201             	 |                              GID_MIN for 'system process users'                               |
| SYS_GID_MAX     | 999             	 |                              GID_MAX for 'system process users'                               |
| CREATE_HOME     | yes             	 |         Whether a user home directory is created as part of the user account creation         |
| UMASK           | 077             	 |          The value for the default permissions assigned to any file a user creates.           |
| USERGROUPS_ENAB | yes             	 |     Whether a group with the same name as the username is created during account creation     |
| ENCRYPT_METHOD  | SHA512          	 |                                  The encryption method used                                   |

- In order for the uid variable to be more safe, one could increase the range for it\'s values by increasing the range of possible values for it.
- Another option to make it more secure would be to make the valus for uid harder to guess, using an algorithm to create pseudo random uid values for uid.
- The theoretical number of users that can be created is defined by the difference between *UID_MAX* and *UID_MIN*. In the above example a maximum of 59000 users could be created. This relationship between the upper and lower limits for the *UID* values and the theoretical number of users that can be created comes from the fact, that every single *uid* has to be uniq. This variable is a *unique key*.

##### Creating a new user 'kate'

```bash
root * groupadd cyclists
root * useradd -g cyclists -d /bin/bash -c "User is a real cyclist, no ebike." -m -d /home/kate kate
root * id kate
uid=1006(kate) gid=1007(cyclists) groups=1007(cyclists)
root * tail -5 /etc/group
tyler:x:1002:
brianna:x:1003:
golfers:x:1005:brianna,veronica
veronica:x:1006:
cyclists:x:1007:
root * tail -5 /etc/passwd
tyler:x:1002:1002::/home/tyler:/bin/bash
brianna:x:1003:1003::/home/brianna:/bin/bash
veronica:x:1004:1006::/home/veronica:/bin/bash
will:x:1005:1005:His wife says, that his handicap is rubbish.:/home/will:/bin/bash
kate:x:1006:1007:User is a real cyclist, no ebike.:/home/kate:/bin/bash
root * tail -5 /etc/shadow
tyler:!!:18987:0:99999:7:::
brianna:!!:18987:0:99999:7:::
veronica:!!:18987:0:99999:7:::
will:$6$tMIEzfVP$IPcfrMzwKeqdpabU0ztOH7znjdFD0wINLY7a0wnw5enjr.CSI1B0sIc723GHHIOqWCN/oroo8.ZlttDIW7nQt1:18987:0:99999:7:::
kate:!!:18987:0:99999:7:::
root * 
```

#### Changing the initiation values for 'kate'

Below are the values for user *kate* after initialisation.

- The third column (`chage -d`) has a value of **18987**. It marks the date, the account password was created, counting the days since 01/01/1970 in this case till creation.
- 

```vim
kate:!!:18987:0:99999:7:::
```

```bash
root * chage -m 5 -M 90 -W 10 -I 3 kate
root * grep "kate" /etc/shadow
kate:!!:18987:5:90:10:3::
root * 
```