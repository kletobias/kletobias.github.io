---
title: 'Linux Course: Module 4'
subtitle: High-fidelity mobile app designs for a super awesome social media company. BEST SUBTITLE
date: 2021-12-18 00:00:00
description: Notes from the Linux course I am taking currently.
accent_color: '#4C60E6'
---

**Important to do: Change skinport to something neutral in all console outputs used in this article.**

**Important to do: Change skinport to something neutral in all console outputs used in this article.**
# Prior to Module 4
You can do this with these commands:

```bash
mkdir learning_c
cd learning_c
touch bspl{0001..0003}.c
```

### Explanation:
---
*   `mkdir learning_c`

    *   This will create a folder called `learning_c` in the current folder
    *   The current folder usually is your home folder also called `~`
    *   You can change the current directory using the `cd` command (i.e. `cd Desktop`)
*   `cd learning_c`

    *   Yes, you can guess it, you're entering on the newly created folder
*   `touch bspl{0001..0003}.c`

    *   `touch` is a tool to create empty files and modify timestamps; we're creating empty files.
    *   `touch myfile` will create an empty file called `myfile`.
    *   The ugly code that follows (`bspl{0001..0003}.c`) is called a **brace expansion**. This is a great feature of the `bash` shell that allows you to create long lists of arbitrary string combinations. You can learn more about this in the [Bash Hackers Wiki](http://wiki.bash-hackers.org/syntax/expansion/brace). In this case you will be making a long list of parameters that will be passed to `touch`. You can also use its long equivalent:

        ```bash
        touch bspl0001.c bspl0002.c bspl0003.c
        ```

    *   You can change the number of files: if you want 12 files, you can run `bspl{0001..0012}.c`.

    *   The leading zeros (`0012` instead of `12`) make sure that the output uses zero\-padded 4 digits.

**Terminal Example**
```bash
[tklein@linux ~]$ touch randomfile{001..010}
[tklein@linux ~]$ ls -ltr
...
-rw-rw-r--. 1 tklein tklein       0 Dec 20 00:40 randomfile010
-rw-rw-r--. 1 tklein tklein       0 Dec 20 00:40 randomfile009
-rw-rw-r--. 1 tklein tklein       0 Dec 20 00:40 randomfile008
-rw-rw-r--. 1 tklein tklein       0 Dec 20 00:40 randomfile007
-rw-rw-r--. 1 tklein tklein       0 Dec 20 00:40 randomfile006
-rw-rw-r--. 1 tklein tklein       0 Dec 20 00:40 randomfile005
-rw-rw-r--. 1 tklein tklein       0 Dec 20 00:40 randomfile004
-rw-rw-r--. 1 tklein tklein       0 Dec 20 00:40 randomfile003
-rw-rw-r--. 1 tklein tklein       0 Dec 20 00:40 randomfile002
-rw-rw-r--. 1 tklein tklein       0 Dec 20 00:40 randomfile001
```
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

Equivalent values for the assignment of permissions using numerical values:
**Number**  | **Permission Type**   | **Symbol** 
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
- `-R` option - will recursively change the ownership in all the subdirectories as well.
 
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

**Raw Output:**

```sh
[tklein@linux tmp]$ su
Password:
[root@linux tmp]# hostname
linux.fritz.box
[root@linux tmp]# touch tx
[root@linux tmp]# ls -l tx
-rw-r--r--. 1 root root 0 Dec 19 12:47 tx
[root@linux tmp]# getfacl tx
# file: tx
# owner: root
# group: root
user::rw-
group::r--
other::r--

[root@linux tmp]# setfacl -m u:tklein:rw /tmp/tx
[root@linux tmp]# setfacl -m u:tklein:r /tmp/tx
[root@linux tmp]# getfacl tx
# file: tx
# owner: root
# group: root
user::rw-
user:tklein:r--
group::r--
mask::r--
other::r--

[root@linux tmp]# setfacl -m u:tklein:rw /tmp/tx
[root@linux tmp]# echo "Changing the acl for the group in the following"
Changing the acl for the group in the following
[root@linux tmp]# setfacl -m g:tklein:rw /tmp/tx
[root@linux tmp]# ls -l tx
-rw-rw-r--+ 1 root root 214 Dec 19 13:31 tx
[root@linux tmp]# getfacl tx
# file: tx
# owner: root
# group: root
user::rw-
user:tklein:rw-
group::r--
group:tklein:rw-
mask::rw-
other::r--

[root@linux tmp]# echo "Number 3"
Number 3
[root@linux tmp]# mkdir -p acl_practice_dir
[root@linux tmp]# mkdir -p acl_practice_dir/nested_dir
[root@linux tmp]# touch acl_practice_dir/nested_dir/new_file
[root@linux tmp]# getfacl acl_practice_dir/
# file: acl_practice_dir/
# owner: root
# group: root
user::rwx
group::r-x
other::r-x

[root@linux tmp]# getfacl acl_practice_dir/nested_dir/
# file: acl_practice_dir/nested_dir/
# owner: root
# group: root
user::rwx
group::r-x
other::r-x

[root@linux tmp]# getfacl acl_practice_dir/nested_dir/new_file
# file: acl_practice_dir/nested_dir/new_file
# owner: root
# group: root
user::rw-
group::r--
other::r--

[root@linux tmp]# setfacl -Rm u:user /tmp/acl_practice_dir
setfacl: Option -m: Invalid argument near character 3
[root@linux tmp]# man setfacl
[root@linux tmp]# setfacl -Rm u:tklein:rw /tmp/acl_practice_dir
[root@linux tmp]# ls -l acl_practice_dir/nested_dir/
total 0
-rw-rw-r--+ 1 root root 0 Dec 19 13:36 new_file
[root@linux tmp]# getfacl acl_practice_dir/nested_dir/
# file: acl_practice_dir/nested_dir/
# owner: root
# group: root
user::rwx
user:tklein:rw-
group::r-x
mask::rwx
other::r-x

[root@linux tmp]# getfacl acl_practice_dir/nested_dir/new_file
# file: acl_practice_dir/nested_dir/new_file
# owner: root
# group: root
user::rw-
user:tklein:rw-
group::r--
mask::rw-
other::r--

[root@linux tmp]# setfacl -x u:tklein tx
[root@linux tmp]# getfacl tx
# file: tx
# owner: root
# group: root
user::rw-
group::r--
group:tklein:rw-
mask::rw-
other::r--

[root@linux tmp]# echo "Set permissions back to default"
Set permissions back to default
[root@linux tmp]# setfacl -b tx
[root@linux tmp]# getfacl tx
# file: tx
# owner: root
# group: root
user::rw-
group::r--
other::r--

[root@linux tmp]# setfacl -m g:tklein:rw /tmp/tx
[root@linux tmp]#

```

From my user account perspective:


```sh
Last login: Sat Dec 18 21:03:02 2021 from desktop-2gc6eav.fritz.box
[tklein@linux ~]$ cd tmp
-bash: cd: tmp: No such file or directory
[tklein@linux ~]$ cd /tmp
[tklein@linux tmp]$ cat tx
[tklein@linux tmp]$ vi tx
[tklein@linux tmp]$ vi tx
[tklein@linux tmp]$ vi tx
[tklein@linux tmp]$ cat tx
iiiijf fijwef iofjofj iojf owiefjeiwfojeiofjweifjijeiwfj
[tklein@linux tmp]$ vi tx
[tklein@linux tmp]$ vi tx
[tklein@linux tmp]$ cat tx
After I changed the user permissions for user tklein via `setfacl -m u:tklein:rw /tmp/tx`, I have the necessary permissions to edit the content of the file.
iiiijf fijwef iofjofj iojf owiefjeiwfojeiofjweifjijeiwfj
[tklein@linux tmp]$ rm tx
rm: cannot remove â€˜txâ€™: Operation not permitted
[tklein@linux tmp]$
```



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

### 63 TAB Completion and Up Arrow Keys

- Hitting TAB key complements the available commands, files or directories.
  - `chm TAB`
  - `ls j<TAB>`
  - `cd Des<TAB>`
- Hitting the up arrow key on the keyboard returns the last command ran.

### 64 Adding Text to Files
*How to populate and empty file.*

- 3 simple ways to add text to a file.
  - **vi**
  - **Redirect command output `>` or `>>`**

Examples for each of the two methods mentioned above:

**vi:**
```bash
touch cramer
vi cramer
---
# Inside vi, one can populate the file with text like, so:
`hit i key`
write: `This is Cramer`
`hit ESC key`
`hit colon button and type wq, hit ENTER`
---
# Back in the shell where one left off, one can type the
# following to verify that the text was written to the 
# file 'cramer'
[tklein@linux ~]$ cat cramer
This is Cramer
```
**Redirecting:**
```bash
[tklein@linux ~]$ echo 'All I want for Christmas is you, is the chorus of a popular Christmas song.' >> Christmasfile
[tklein@linux ~]$ cat Christmasfile
All I want for Christmas is you, is the chorus of a popular Christmas song.
[tklein@linux ~]$

```
If nothing is yet written to the file that one writes the
text in it does not matter, if `>` or `>>` is used to redirect.

If however there is already text in the file, prior to one writing additional text in it, the newly added text will overwrite the existing text and replace it.
- `>>` should be used, if one does not want to replace everything that was already written to the file with the newly added text.
- `>` can be used, if one is fine with the newly added text replacing the already existing text in the file that is written to.
- It does not matter which option is used, in the case of a newly created and empty file. See above for details.

### 65 Input and Output Redirects

- There are 3 redirects in Linux
	1. Standard input (**stdin**) and it has file descriptor number as 0
	2. Standard output (**stdout**) and it has file descriptor number as 1
	3. Standard error (**stderr**) and it has file descriptor number as 2

- Output (**stdout**) - 1
  - By default when running a command it's output goes to the terminal.
  - The output of a command can be routed to a file using `>` symbol.
    - E.g. `ls -l > listings`
    - E.g. `pwd \> findpath` 
  - If using the same file for additional output or to append to the same file then use `>>`
    - E.g. `ls -la >> listings`
    - E.g. `echo 'Hello World' >> findpath`



**Terminal Example**
```bash
[tklein@linux ~]$ pwd
/home/tklein
[tklein@linux ~]$ ls -la > homedirlisting
# Shows the listing of the home directory 
# and overwrites any existing content of the file.
[tklein@linux ~]$ cat homedirlisting
# Append to the previous input
[tklein@linux ~]$ ls -ltr >> homedirlisting
# cat 'homedirlisting' again to verify it was appended.
[tklein@linux ~]$ cat homedirlisting
# Overwriting what was previously written
# to the file 'homedirlisting'
[tklein@linux ~]$ echo 'Christmas is around the corner.' > homedirlisting
[tklein@linux ~]$ cat homedirlisting
Christmas is around the corner.
[tklein@linux ~]$
```


- Input (**stdin**) - 0
  - Input is used when feeding file contents to a file.
    - E.g. `cat < listings` - cat takes listings as input.
    - E.g. `mail -s 'Office memo' allusers@bestmail.com < memoletter`

- Error (**stderr**) - 2
	- When a command is executed we use a keyboard and that is also considered (**stdin - 0**)
	- That command ouput goes on the monitor and that output is (**stdout -  1**)
	- If the command produced any error on the screen then it is considered (**stderr - 2**)
		- We can use redirects to route errors from the screen.
			- E.g. `ls -l /root 2> errorfile`
			- E.g. `telnet localhost 2> errorfile`



**Terminal Example**
```bash
# The following command gives errors as output.
[tklein@linux ~]$ telnet localhost
Trying ::1...
telnet: connect to address ::1: Connection refused
Trying 127.0.0.1...
telnet: connect to address 127.0.0.1: Connection refused
# These two errors qualify as 'stderr - 2' and so can be
# redirected to any textfile and will not appear on screen,
# if redirected.
[tklein@linux ~]$ telnet localhost 2> errorfile
Trying ::1...
Trying 127.0.0.1...
[tklein@linux ~]$ cat errorfile
telnet: connect to address ::1: Connection refused
telnet: connect to address 127.0.0.1: Connection refused
[tklein@linux ~]$
```

### 66 Standard Output to a File (`tee`)

- `tee` command is used to store and view (both at the same time) the output of any command.
- The command is named after the T-splitter used in plumbing. It basically breaks the output of a program so that it can be both displayed on screen and saved in a file. It does both simultaneously. It copies the result into the specified files or variabless and also display the result. 

**Terminal Example**
```bash
[tklein@linux ~]$ echo 'Christmas only happens once a year.' | tee christmas_truths
Christmas only happens once a year.
[tklein@linux ~]$ cat christmas_truths
Christmas only happens once a year.
[tklein@linux ~]$ rm christmas_truths
[tklein@linux ~]$ echo 'Christmas only happens once a year.' | tee christmas_truths
Christmas only happens once a year.
[tklein@linux ~]$ cat christmas_truths
Christmas only happens once a year.
# The tee command replaces existing text already present in the file,
# if used without an option.
[tklein@linux ~]$ echo 'Christmas only happens once a year. We believe so.' | tee christmas_truths
Christmas only happens once a year. We believe so.
[tklein@linux ~]$ cat christmas_truths
Christmas only happens once a year. We believe so.
# Using option `-a` the text gets appended instead.
[tklein@linux ~]$ echo 'Christmas only happens once a year.' | tee -a christmas_truths
Christmas only happens once a year.
[tklein@linux ~]$ cat christmas_truths
Christmas only happens once a year. We believe so.
Christmas only happens once a year.
```


```bash
# text input can be redirected to multiple files at once.
# These files do not have to exist prior to running the
# command `tee`.
[tklein@linux ~]$ ls -l | tee file1 file2 file3
```


**Misc.**

```bash
# The version of a command can be looked up by entering the command:
# `<command> --version`
[tklein@linux ~]$ tee --version
tee (GNU coreutils) 8.22
Copyright (C) 2013 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Written by Mike Parker, Richard M. Stallman, and David MacKenzie.
[tklein@linux ~]$
```


```bash
# The word count in a text file can be looked up by using command
# `wc -c <file>``
[tklein@linux ~]$ wc -c christmas_truths
87 christmas_truths
```

### 67 Pipes (**|**)


- A pipe is used by the shell to connect the ouput of one command directly to the input of another command.
- The symbol for a pipe is the vertical bar (**|**).
- The structure of a pipe command looks like this:
  - `command1 [arguments] | command2 [arguments]`
  - E.g. `ls -l | <command2> [arguments]`

### 68 File Maintainance Commands
(`cp`,`rm`,`mv`,`mkdir`,`rmdir`)

**Overview of the commands, that are part of this chapter:**

- `cp`
  - Copies files and directories.
  - Basic structure of the command is among others:
      `cp [OPTION] SOURCE DEST`
  - If one wants to copy an entire directory to another one, the `-R` or `-r` option has to be included in the command for it to copy the source directory recursively to the destination directory.
- `rm`
  - Lets the user remove (delete) files or directories.
  - The command is destructive and must be used with great care, especially when using the following options:
    - `-f` or `--force` never prompts the user before something is removed.
    - `-r`, `-R` or `--recursive` removes directories and their contents recursively.
    - Any combination of the above commands, including none of them together with wildcards.
  - The command has several options that can act as a safety net, so the user gets prompts, warnings or more control over how verbose the command is once executed. This can reduce the danger of involuntarily removing essential files and directories of the system. See `man rm` for details.
- `mv`
  - moves or renames files.
  - `mv [OPTION]... [-T] SOURCE DEST` 
    - With `-T`, it treats the `DEST` as a regular file and not as a 	directory.
    - It renames `SOURCE` to `DEST`
        - Example that also shows that it works without using `-T` as well.
		          As illustrated below. One just can't specify a directory as `DEST` for it to work.
				  It also shows that only the file name gets changed, the content of the original file remains the same:
	    ```bash
		[tklein@linux ~]$ ls -ltr david*
		-r--r--r--. 1 tklein tklein 0 Dec 20 06:21 david
		[tklein@linux ~]$ echo "This file documents the endevour of finding david's last name" > david
		-bash: david: Permission denied
		[tklein@linux ~]$ su
		Password:
		[root@linux tklein]# chmod 771 david
		[root@linux tklein]# ls -ltr david
		-rwxrwx--x. 1 tklein tklein 0 Dec 20 06:21 david
		[root@linux tklein]# exit
		exit
		[tklein@linux ~]$ whoami
		tklein
		[tklein@linux ~]$ echo "This file documents the endevour of finding david's last name" > david
		[tklein@linux ~]$ cat david
		This file documents the endevour of finding david's last name
		[tklein@linux ~]$ cp david david_2
		[tklein@linux ~]$ mv -T david david_hasselhof
		[tklein@linux ~]$ cat david_hasselhof
		This file documents the endevour of finding david's last name
		[tklein@linux ~]$ mv david_2 david
		[tklein@linux ~]$ rm david_hasselhof
		[tklein@linux ~]$ mv david david_hasselhoff
		[tklein@linux ~]$ cat david_hasselhoff
		This file documents the endevour of finding david's last name
		[tklein@linux ~]$
		```
			
	


  - `mv [OPTION]... SOURCE... DIRECTORY` 
  	- Like this, it moves `SOURCE` to `DIRECTORY`
	- Example:
	    ```bash
		[tklein@linux ~]$ ls -ltr
		total 9284
		...
		drwxrwxr-x. 2 tklein tklein      67 Dec 20 13:00 seinfeld
		drwxrwxr-x. 2 tklein tklein      67 Dec 20 13:02 seinfelds_backup_plan
		-rw-rw-r--. 1 tklein tklein       0 Dec 20 22:25 seinfelds_secret_plan
		[tklein@linux ~]$ mv seinfelds_secret_plan seinfeld
		[tklein@linux ~]$ ls -ltr seinfeld
		total 0
		-rw-rw-r--. 1 tklein tklein 0 Dec 20 12:58 seinfelds_fave_file
		-rw-rw-r--. 1 tklein tklein 0 Dec 20 12:59 seinfelds_second_fave_file
		-rw-rw-r--. 1 tklein tklein 0 Dec 20 22:25 seinfelds_secret_plan
		[tklein@linux ~]$
		```