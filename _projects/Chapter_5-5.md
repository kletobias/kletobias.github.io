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

The command has the following important options. It is a command that is designed to be used for an individual user,
in the way it is shown here. In a corporate environment much this is automated, so one does not have to define values for each user that has to be created. Default values are used instead.

|    Label    | -m      | -M      | -d      | -I       | -E              | -W       | User     |
|:-----------:|---------|---------|---------|----------|-----------------|----------|----------|
| Description | mindays | maxdays | lastday | inactive | expiration date | warndays | username |
|   Example   |         |         |         |          |                 |          |          |


| Label | Description     | Example |
|-------|-----------------|---------|
| -m    | MIN DAYS        |         |
| -M    | MAX DAYS        |         |
| -d    | LAST DAY        |         |
| -I    | INACTIVE        |         |
| -E    | EXPIRATION DATE |         |
| -W    | PASS_WARN_AGE   |         |
| User  | USERNAME        |         |


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
UID_MIN         1000 # This is the lower limit for uid
UID_MAX         60000 # Similarly, this is the upper limit for uid
SYS_UID_MIN     201 # This variable is used for any user that is a 'system process user'
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

| Variable        |     Example	      |
|-----------------|:-----------------:|
| MAIL_DIR        | /var/spool/mail 	 |
| PASS_MAX_DAYS   | 99999           	 |
| PASS_MIN_DAYS   | 0               	 |
| PASS_MIN_LEN    | 5               	 |
| PASS_WARN_AGE   | 7               	 |
| UID_MIN         | 1000            	 |
| UID_MAX         | 60000           	 |
| SYS_UID_MIN     | 201             	 |
| SYS_UID_MAX     | 999             	 |
| GID_MIN         | 1000            	 |
| GID_MAX         | 60000           	 |
| SYS_GID_MIN     | 201             	 |
| SYS_GID_MAX     | 999             	 |
| CREATE_HOME     | yes             	 |
| UMASK           | 077             	 |
| USERGROUPS_ENAB | yes             	 |
| ENCRYPT_METHOD  | SHA512          	 |

- The theoretical number of users that can be created is defined by the difference between *UID_MAX* and *UID_MIN*. In the above example a maximum of 59000 users could be created. This relationship between the upper and lower limits for the *UID* values and the theoretical number of users that can be created comes from the fact, that every single *uid* has to be uniq. This variable is a *unique key*.

