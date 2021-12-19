---
title: Linux Course: Module 4
subtitle: High-fidelity mobile app designs for a super awesome social media company. BEST SUBTITLE
date: 2021-12-18 00:00:00
description: Notes from the Linux course I am taking currently.
accent_color: '#4C60E6'
---

**Important to do: Change skinport to something neutral in all console outputs used in this article.**

# Module 4

## `chmod`
- To give user who is owner of the file write permissions for file 'jerry', type `chmod u+w jerry`
- To revoke write permissions, type `chmod u-w jerry`
- read permissions for group: `chmod g+r jerry` / to revoke them: `chmod g-r jerry`
- For 'others' give/revoke read and write: `chmod o+rw jerry` / `chmod o-rw jerry`
- check what the permissions are after using each one of the above commands: `ls -ltr jerry`
- All together there are the following 'groups' one can specify permissions for:
	- 'u' - explanation: 'user', owner of the object, U in the following set theory illustration.
	- 'g' - explanation: 'group', group of the owner, *G in the following, as per set theory notation.*
	- 'o' - explanation:	'other', set of $\left(U \cup G \right)^c=O$, *O, in capital letter, as per set theory notation.*
	- 'a' - explanation: 'all', set of $(U \cup G \cup O) = A$, *Capital A, see above for explanation.*
- Same with 'x', giving u,g or o execute rights and using `chmod u+x jerry` and for the other two analogously.

### About 'x' permission on directories

- `drwxrwxr-x. 2 tklein tklein    6 Dec 10 11:44 seinfeld` -> means one is allowed to cd into the directory for example.

```sh
[tklein@linux seinfeld]$ chmod a-x seinfeld
chmod: cannot access ‘seinfeld’: No such file or directory
[tklein@linux seinfeld]$ cd
[tklein@linux ~]$ chmod a-x seinfeld
[tklein@linux ~]$ cd seinfeld
-bash: cd: seinfeld: Permission denied
[tklein@linux ~]$
```

## Assigning permissions using numerical values

Equivalent values for the assignment of permissions using numerical values are:

| Number | Permission Type        | Symbol |
|--------|------------------------|--------|
| 0      | No permission          | \-\-\- |
| 1      | Execute                | \-\-x    |
| 2      | Write                  | \-w\-    |
| 3      | Execute \+ Write        | \-wx    |
| 4      | Read                   | r\-\-    |
| 5      | Read \+ Execute         | r\-x    |
| 6      | Read \+ Write           | rw\-    |
| 7      | Read \+ Write + Execute | rwx    |

~~**Note:** The order in which permissions `read`, `write` and `execute` are given in column **Symbol** are given is sorted ascending (rwx). It follows the equivalent numerical values of the respective commands. $rwx = 421$. It is also, $4$, $4+2=6$, $4+1=5$ and $4+2+1=7$, which is $0$, $2$ and $1$, modulo 3. So all combinations with `read` are simply $0, 1, 2$ mod 3. And any combination that has read permissions, is an integer, a fraction of $4/2$. So read, is double of write and write double of execute.~~

| variable    | count  | mean   | std   | min  | 10%   | 25%   | 50%    | 75%   | 90%   | max   |
|-------------|--------|--------|-------|------|-------|-------|--------|-------|-------|-------|
| einbau_kue  | 9480.0 | 0.61   | 0.49  | 0.0  | 0.0   | 0.0   | 1.0    | 1.0   | 1.0   | 1.0   |
| lift        | 9480.0 | 0.21   | 0.41  | 0.0  | 0.0   | 0.0   | 0.0    | 0.0   | 1.0   | 1.0   |
| nebenkosten | 9480.0 | 159.08 | 83.13 | 0.0  | 73.0  | 100.0 | 144.96 | 200.0 | 265.0 | 950.0 |
| lat         | 9480.0 | 53.57  | 0.05  | 53.4 | 53.49 | 53.55 | 53.58  | 53.6  | 53.62 | 53.71 |
| lng         | 9480.0 | 10.01  | 0.09  | 9.74 | 9.9   | 9.96  | 10.01  | 10.07 | 10.13 | 10.3  |

## File Ownership Commands (`chown`, `chgrp`)
[Video number 60](https://www.udemy.com/course/complete-linux-training-course-to-get-your-dream-it-job/learn/lecture/9165554#notes)

- `chown` - stands for change ownership.
- `chgrp` - stands for change group.

```sh
[root@linux tklein]# ls -ltr
total 9212
drwxr-xr-x. 2 tklein tklein       6 Dec  3 17:56 Videos
drwxr-xr-x. 2 tklein tklein       6 Dec  3 17:56 Templates
drwxr-xr-x. 2 tklein tklein       6 Dec  3 17:56 Public
drwxr-xr-x. 2 tklein tklein       6 Dec  3 17:56 Pictures
drwxr-xr-x. 2 tklein tklein       6 Dec  3 17:56 Music
drwxr-xr-x. 2 tklein tklein       6 Dec  3 17:56 Downloads
drwxr-xr-x. 2 tklein tklein       6 Dec  3 17:56 Documents
drwxr-xr-x. 2 tklein tklein       6 Dec  3 17:56 Desktop
-rw-rw-r--. 1 tklein tklein       0 Dec  4 05:55 cramer
drwxrwxr-x. 2 tklein tklein    4096 Dec  4 05:58 logs
drwxrwxr-x. 2 tklein tklein      54 Dec  4 06:05 config
drwxrwxr-x. 2 tklein tklein      47 Dec  4 06:14 lecture_notes
-rw-rw-r--. 1 tklein tklein       0 Dec  4 06:15 kramer
-rw-rw-r--. 1 tklein tklein       0 Dec  4 06:15 jerry
-r--r--r--. 1 tklein tklein       0 Dec  4 06:15 george
-rw-rw-r--. 1 tklein tklein       0 Dec  4 06:42 susan
-rw-rw-r--. 1 tklein tklein       0 Dec 10 11:42 bart
drwxrwxr-x. 2 tklein tklein       6 Dec 10 15:14 seinfeld
```
- The third column gives the name of the owner, it is a username. Here it is *tklein* or *root*.
- The fourth column gives the name of the group, that is the owner. Here it is *tklein* or *root*.

```sh
[root@linux tklein]# chown root susan
[root@linux tklein]# ls -ltr susan
-rw-rw-r--. 1 root tklein 0 Dec  4 06:42 susan

[root@linux tklein]# exit

[tklein@linux ~]$ ls -l susan
-rw-rw-r--. 1 root tklein 0 Dec  4 06:42 susan
[tklein@linux ~]$ chgrp root susan
chgrp: changing group of ‘susan’: Operation not permitted
[tklein@linux ~]$ su
Password:
[root@linux tklein]# chgrp root susan
[root@linux tklein]# ls -ltr susan
-rw-rw-r--. 1 root root 0 Dec  4 06:42 susan
[root@linux tklein]#
```

**Creating a test file to practice changing ownership of the file.**
```sh
# going into my home directory
[tklein@linux /]$ cd /home/tklein
# Creating an empty file 'permissiontestfile'
[tklein@linux ~]$ touch permissiontestfile
# Checking who owns the file and which group owns it.
[tklein@linux ~]$ ls -ltr permissiontestfile
# 'tklein', me is the owner and the group who owns it.
-rw-rw-r--. 1 tklein tklein 0 Dec 18 21:17 permissiontestfile 
# I try to change the ownership to the user 'root', using my account 'tklein'
[tklein@linux ~]$ chown root permissiontestfile
# I do not have the permissions to change the ownership.
chown: changing ownership of ‘permissiontestfile’: Operation not permitted
# I need to become 'root' in order to change the ownership.
[tklein@linux ~]$ su
Password:
# Now that I am 'root', I can change the ownership to 'root'.
[root@linux tklein]# chown root permissiontestfile
# Checking, if the changes were recorded and that now 'root' is the new owner.
[root@linux tklein]# ls -ltr permissiontestfile
# Indeed 'root' is the new owner of the file.
-rw-rw-r--. 1 root tklein 0 Dec 18 21:17 permissiontestfile
# Becoming my user account again.
[root@linux tklein]# exit
exit
# Again, permission denied when I try to change ownership while not being 'root'.
[tklein@linux ~]$ chown tklein permissiontestfile
chown: changing ownership of ‘permissiontestfile’: Operation not permitted
[tklein@linux ~]$ su
Password:
# Being root, I change the ownership back to my account.
[root@linux tklein]# chown tklein permissiontestfile
[root@linux tklein]# exit
exit
[tklein@linux ~]$ ls -ltr permissiontestfile
-rw-rw-r--. 1 tklein tklein 0 Dec 18 21:17 permissiontestfile
# I can change permissions using my account, who owns the file.
[tklein@linux ~]$ chmod 751 permissiontestfile
[tklein@linux ~]$ ls -ltr permissiontestfile
-rwxr-x--x. 1 tklein tklein 0 Dec 18 21:17 permissiontestfile
[tklein@linux ~]$
```
TODO remove the number of the videos for the website version!

## 61 Access Control List (ACL)

**Use Case for ACL**
ACL = Access Control List

A file created by root and a user needs to be able to read it. He is not part of the group either. Only this one user should be able to read it, no one else. It is a flexible permission setting mechanism.

**The List of commands for setting up ACL**

1. To add permission for user.
	`setfacl -m u:user:rwx /path/to/file`
	`setfacl` = Set file ACL
	`-m` to modify the permissions
	`-u:user` for the user permissions are altered for.
2. To add permissions for a group.
	`setfacl -m g:group:rw /path/to/file`
3. To allow all files or directories to inherit ACL entries from the directory it is within.
	`setfacl -Rm "entry" /path/to/dir`
	`-R` For recursively applying the changes.
4. To remove a specific entry.
	`setfacl -x u:user /path/to/file` (For a specific user)
	`-x` for removal

**Note:**
- As you assign the ACL permission to a file/directory it adds `+` sign at the end of the permission.

### 62 Help Commands

*Primer:*
[unix - How to denote that a command line argument is optional when printing usage - Stack Overflow](https://stackoverflow.com/questions/21503865/how-to-denote-that-a-command-line-argument-is-optional-when-printing-usage/21504030)

- square brackets `[optional option]`
- angle brackets `<required argument>`
- curly braces `{default values}`
- parenthesis `(miscellaneous info)`

#### Types of Help Commands
*There are three types of help commands*
- `whatis <command>`
- `<command> --help`
- `man <command>`
