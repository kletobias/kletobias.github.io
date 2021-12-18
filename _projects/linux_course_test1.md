---
title: Linux Course: Module 4
subtitle: High-fidelity mobile app designs for a super awesome social media company. BEST SUBTITLE
date: 2021-12-18 00:00:00
description: Notes from the Linux course I am taking currently.
featured_image:
accent_color: '#4C60E6'
gallery_images:
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

```bash
[tklein@linux seinfeld]$ chmod a-x seinfeld
chmod: cannot access ‘seinfeld’: No such file or directory
[tklein@linux seinfeld]$ cd
[tklein@linux ~]$ chmod a-x seinfeld
[tklein@linux ~]$ cd seinfeld
-bash: cd: seinfeld: Permission denied
[tklein@linux ~]$
``` 

## Assigning permissions using numerical values

Equivalent values for the assignment of permissions using numerical values:
  
Number  | Permission Type   | Symbol 
--|---|-- 
0  | No permission  | --- 
1  | Execute  |  --x 
2  | Write  |  -w- 
3  | Execute + Write  | -wx 
4  | Read  | r-- 
5  | Read + Execute  | r-x 
6  | Read + Write  | rw- 
7  | Read + Write + Execute  | rwx
 
~~**Note:** The order in which permissions `read`, `write` and `execute` are given in column **Symbol** are given is sorted ascending (rwx). It follows the equivalent numerical values of the respective commands. $rwx = 421$. It is also, $4$, $4+2=6$, $4+1=5$ and $4+2+1=7$, which is $0$, $2$ and $1$, modulo 3. So all combinations with `read` are simply $0, 1, 2$ mod 3. And any combination that has read permissions, is an integer, a fraction of $4/2$. So read, is double of write and write double of execute.~~

## File Ownership Commands (`chown`, `chgrp`)
 [Video number 60](https://www.udemy.com/course/complete-linux-training-course-to-get-your-dream-it-job/learn/lecture/9165554#notes)

- `chown` - stands for change ownership.
- `chgrp` - stands for change group.
```bash
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
-rw-r--r--. 1 root   root       196 Dec 10 18:59 skinport_api_cred_url
-r-x--x--x. 1 root   root        86 Dec 10 19:03 v1
-rw-r--r--. 1 root   root       135 Dec 10 19:24 curl_skinport_header_file
-rw-r--r--. 1 root   root       135 Dec 10 19:31 curl_skinport_script_backup.sh
-rw-r--r--. 1 root   root       351 Dec 10 19:38 backup_complete_api_skinport_request
-rw-r--r--. 1 root   root       176 Dec 10 19:45 basic_auth
-rw-r--r--. 1 root   root        79 Dec 10 19:50 complete_api_skinport_request
-rw-r--r--. 1 root   root        86 Dec 10 19:52 complete_api_skinport_request_test_new-lines
-rw-r--r--. 1 root   root   9392679 Dec 10 20:40 api_output_skinport.json
```
- The third column gives the name of the owner, it is a username. Here it is *tklein* or *root*.
- The fourth column gives the name of the group, that is the owner. Here it is *tklein* or *root*.

```bash
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
