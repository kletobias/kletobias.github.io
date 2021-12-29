---
title: 'Linux Course: Module 4 Notes'
subtitle: 'Notes and Examples.'
date: 2021-12-26 00:00:00
description: 'This article covers some of the most essential commands used in any Linux distribution. CentOS 7 was the OS used in the following, it was a virtual machine and accessed through ssh.'
featured_image: 80sterminal.png
gallery_images: Bash_GNOME_Terminal_screenshot.png
accent_color: '#4ce6b8'
---

**Important to do: Change skinport to something neutral in all console outputs used in this article.**

# Prior to Module 4

You can do this with these commands:

```bash
mkdir learning_c
```
```bash
cd learning_c
touch bspl{0001..0003}.c
```

# Module 4

TODO Change inline math that is not rendered correctly on the website to something else.

## `chmod`

-   To give user who is owner of the file write permissions for file 'jerry', type `chmod u+w jerry`
-   To revoke write permissions, type `chmod u-w jerry`
-   read permissions for group: `chmod g+r jerry` / to revoke them: `chmod g-r jerry`
-   For 'others' give/revoke read and write: `chmod o+rw jerry` / `chmod o-rw jerry`
-   check what the permissions are after using each one of the above commands: `ls -ltr jerry`
-   All together there are the following 'groups' one can specify permissions for:
    		\- 'u' - explanation: 'user', owner of the object, U in the following set theory illustration.
    		\- 'g' - explanation: 'group', group of the owner, _G in the following, as per set theory notation._
    		\- 'o' - explanation:	'other', set of $\\left(U \\cup G \\right)^c=O$, _O, in capital letter, as per set theory notation._
    		\- 'a' - explanation: 'all', set of $(U \\cup G \\cup O) = A$, _Capital A, see above for explanation._
-   Same with 'x', giving u,g or o execute rights and using `chmod u+x jerry` and for the other two analogously.

### About 'x' permission on directories

-   `drwxrwxr-x. 2 tklein tklein    6 Dec 10 11:44 seinfeld` -> means one is allowed to cd into the directory for example.

```bash
~ $ chmod a-x seinfeld
chmod: cannot access ‘seinfeld’: No such file or directory
~ $ cd
~ $ chmod a-x seinfeld
~ $ cd seinfeld
-bash: cd: seinfeld: Permission denied
~ $
```

## Assigning permissions using numerical values

Equivalent values for the assignment of permissions using numerical values:

| Number | Permission Type        | Symbol |
| ------ | ---------------------- | ------ |
| 0      | No permission          | ---    |
| 1      | Execute                | --x    |
| 2      | Write                  | -w-    |
| 3      | Execute + Write        | -wx    |
| 4      | Read                   | r--    |
| 5      | Read + Execute         | r-x    |
| 6      | Read + Write           | rw-    |
| 7      | Read + Write + Execute | rwx    |

~~**Note:** The order in which permissions `read`, `write` and `execute` are given in column **Symbol** are given is sorted ascending (rwx). It follows the equivalent numerical values of the respective commands. $rwx = 421$. It is also, $4$, $4+2=6$, $4+1=5$ and $4+2+1=7$, which is $0$, $2$ and $1$, modulo 3. So all combinations with `read` are simply $0, 1, 2$ mod 3. And any combination that has read permissions, is an integer, a fraction of $4/2$. So read, is double of write and write double of execute.~~

## File Ownership Commands (`chown`, `chgrp`)

 [Video number 60](https://www.udemy.com/course/complete-linux-training-course-to-get-your-dream-it-job/learn/lecture/9165554#notes)

-   `chown` - stands for change ownership.
-   `chgrp` - stands for change group.
-   `-R` option - will recursively change the ownership in all the subdirectories as well.

```bash
root $ ls -ltr
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

-   The third column gives the name of the owner, it is a username. Here it is _tklein_ or _root_.
-   The fourth column gives the name of the group, that is the owner. Here it is _tklein_ or _root_.

```bash
root $ chown root susan
root $ ls -ltr susan
-rw-rw-r--. 1 root tklein 0 Dec  4 06:42 susan

root $ exit

~ $ ls -l susan
-rw-rw-r--. 1 root tklein 0 Dec  4 06:42 susan
~ $ chgrp root susan
chgrp: changing group of ‘susan’: Operation not permitted
~ $ su
Password:
root $ chgrp root susan
root $ ls -ltr susan
-rw-rw-r--. 1 root root 0 Dec  4 06:42 susan
root $
```

**Creating a test file to practice changing ownership of the file.**

```bash
# going into my home directory
~ $ cd /home/tklein
# Creating an empty file 'permissiontestfile'
~ $ touch permissiontestfile
# Checking who owns the file and which group owns it.
~ $ ls -ltr permissiontestfile
# 'tklein', me is the owner and the group who owns it.
-rw-rw-r--. 1 tklein tklein 0 Dec 18 21:17 permissiontestfile
# I try to change the ownership to the user 'root', using my account 'tklein'
~ $ chown root permissiontestfile
# I do not have the permissions to change the ownership.
chown: changing ownership of ‘permissiontestfile’: Operation not permitted
# I need to become 'root' in order to change the ownership.
~ $ su
Password:
# Now that I am 'root', I can change the ownership to 'root'.
root $ chown root permissiontestfile
# Checking, if the changes were recorded and that now 'root' is the new owner.
root $ ls -ltr permissiontestfile
# Indeed 'root' is the new owner of the file.
-rw-rw-r--. 1 root tklein 0 Dec 18 21:17 permissiontestfile
# Becoming my user account again.
root $ exit
exit
# Again, permission denied when I try to change ownership while not being 'root'.
~ $ chown tklein permissiontestfile
chown: changing ownership of ‘permissiontestfile’: Operation not permitted
~ $ su
Password:
# Being root, I change the ownership back to my account.
root $ chown tklein permissiontestfile
root $ exit
exit
~ $ ls -ltr permissiontestfile
-rw-rw-r--. 1 tklein tklein 0 Dec 18 21:17 permissiontestfile
# I can change permissions using my account, who owns the file.
~ $ chmod 751 permissiontestfile
~ $ ls -ltr permissiontestfile
-rwxr-x--x. 1 tklein tklein 0 Dec 18 21:17 permissiontestfile
~ $
```

TODO remove the number of the videos for the website version!

## 61 Access Control List (ACL)

**Use Case for ACL**
ACL = Access Control List

A file created by root and a user needs to be able to read it. He is not part of the group either. Only this one user should be able to read it, no one else. It is a flexible permission setting mechanism.

**The List of commands for setting up ACL**

1.  To add permission for user.
    `setfacl -m u:user:rwx /path/to/file`
    `setfacl` = Set file ACL
    `-m` to modify the permissions
    `-u:user` for the user permissions are altered for.
2.  To add permissions for a group.
    `setfacl -m g:group:rw /path/to/file`
3.  To allow all files or directories to inherit ACL entries from the directory it is within.
    `setfacl -Rm "entry" /path/to/dir`
    `-R` For recursively applying the changes.
4.  To remove a specific entry.
    `setfacl -x u:user /path/to/file` (For a specific user)
    `-x` for removal

**Note:**

-   As you assign the ACL permission to a file/directory it adds `+` sign at the end of the permission.

**Raw Output:**

```bash
~ $ su
Password:
root $ hostname
linux.fritz.box
root $ touch tx
root $ ls -l tx
-rw-r--r--. 1 root root 0 Dec 19 12:47 tx
root $ getfacl tx
# file: tx
# owner: root
# group: root
user::rw-
group::r--
other::r--

root $ setfacl -m u:tklein:rw /tmp/tx
root $ setfacl -m u:tklein:r /tmp/tx
root $ getfacl tx
# file: tx
# owner: root
# group: root
user::rw-
user:tklein:r--
group::r--
mask::r--
other::r--

root $ setfacl -m u:tklein:rw /tmp/tx
root $ echo "Changing the acl for the group in the following"
Changing the acl for the group in the following
root $ setfacl -m g:tklein:rw /tmp/tx
root $ ls -l tx
-rw-rw-r--+ 1 root root 214 Dec 19 13:31 tx
root $ getfacl tx
# file: tx
# owner: root
# group: root
user::rw-
user:tklein:rw-
group::r--
group:tklein:rw-
mask::rw-
other::r--

root $ echo "Number 3"
Number 3
root $ mkdir -p acl_practice_dir
root $ mkdir -p acl_practice_dir/nested_dir
root $ touch acl_practice_dir/nested_dir/new_file
root $ getfacl acl_practice_dir/
# file: acl_practice_dir/
# owner: root
# group: root
user::rwx
group::r-x
other::r-x

root $ getfacl acl_practice_dir/nested_dir/
# file: acl_practice_dir/nested_dir/
# owner: root
# group: root
user::rwx
group::r-x
other::r-x

root $ getfacl acl_practice_dir/nested_dir/new_file
# file: acl_practice_dir/nested_dir/new_file
# owner: root
# group: root
user::rw-
group::r--
other::r--

root $ setfacl -Rm u:user /tmp/acl_practice_dir
setfacl: Option -m: Invalid argument near character 3
root $ man setfacl
root $ setfacl -Rm u:tklein:rw /tmp/acl_practice_dir
root $ ls -l acl_practice_dir/nested_dir/
total 0
-rw-rw-r--+ 1 root root 0 Dec 19 13:36 new_file
root $ getfacl acl_practice_dir/nested_dir/
# file: acl_practice_dir/nested_dir/
# owner: root
# group: root
user::rwx
user:tklein:rw-
group::r-x
mask::rwx
other::r-x

root $ getfacl acl_practice_dir/nested_dir/new_file
# file: acl_practice_dir/nested_dir/new_file
# owner: root
# group: root
user::rw-
user:tklein:rw-
group::r--
mask::rw-
other::r--

root $ setfacl -x u:tklein tx
root $ getfacl tx
# file: tx
# owner: root
# group: root
user::rw-
group::r--
group:tklein:rw-
mask::rw-
other::r--

root $ echo "Set permissions back to default"
Set permissions back to default
root $ setfacl -b tx
root $ getfacl tx
# file: tx
# owner: root
# group: root
user::rw-
group::r--
other::r--

root $ setfacl -m g:tklein:rw /tmp/tx
root $
```

From my user account perspective:

```bash
Last login: Sat Dec 18 21:03:02 2021 from desktop-2gc6eav.fritz.box
~ $ cd tmp
-bash: cd: tmp: No such file or directory
~ $ cd /tmp
~ $ cat tx
~ $ vi tx
~ $ vi tx
~ $ vi tx
~ $ cat tx
iiiijf fijwef iofjofj iojf owiefjeiwfojeiofjweifjijeiwfj
~ $ vi tx
~ $ vi tx
~ $ cat tx
After I changed the user permissions for user tklein via `setfacl -m u:tklein:rw /tmp/tx`, I have the necessary permissions to edit the content of the file.
iiiijf fijwef iofjofj iojf owiefjeiwfojeiofjweifjijeiwfj
~ $ rm tx
rm: cannot remove â€˜txâ€™: Operation not permitted
~ $
```

### 62 Help Commands

_Primer:_
[unix - How to denote that a command line argument is optional when printing usage - Stack Overflow](https://stackoverflow.com/questions/21503865/how-to-denote-that-a-command-line-argument-is-optional-when-printing-usage/21504030)

-   square brackets `[optional option]`
-   angle brackets `<required argument>`
-   curly braces `{default values}`
-   parenthesis `(miscellaneous info)`

#### Types of Help Commands

There are three types of help commands

-   `whatis <command>`
-   `<command> --help`
-   `man <command>`

### 63 TAB Completion and Up Arrow Keys

-   Hitting TAB key complements the available commands, files or directories.
    -   `chm TAB`
    -   `ls j<TAB>`
    -   `cd Des<TAB>`
-   Hitting the up arrow key on the keyboard returns the last command ran.

### 64 Adding Text to Files

How to populate an empty file.

-   3 simple ways to add text to a file.
    -   `vi <file>`
    -   Redirect command output `>` or `>>`

Examples for each of the two methods mentioned above:

**vi\:**

```bash
touch cramer
vi cramer
```

Inside vi, one can populate the file with text like, so\:

-   hit i key
-   write\: This is Cramer
-   hit ESC key
-   hit colon key and type wq, hit ENTER
-   Back in the shell where one left off, one can type the following to verify that the text was written to the file 'cramer'

```bash
~ $ cat cramer
This is Cramer
~ $
```

**Redirecting\:**

```bash
~ $ echo 'All I want for Christmas is you, is the chorus of a popular Christmas song.' >> Christmasfile
~ $ cat Christmasfile
All I want for Christmas is you, is the chorus of a popular Christmas song.
~ $
```

If nothing is yet written to the file that one writes the text in it does not matter, if `>` or `>>` is used to redirect.

If however there is already text in the file, prior to one writing additional text in it, the newly added text will overwrite the existing text and replace it.

-   `>>` should be used, if one does not want to replace everything that was already written to the file with the newly added text.
-   `>` can be used, if one is fine with the newly added text replacing the already existing text in the file that is written to.
-   It does not matter which option is used, in the case of a newly created and empty file. See above for details.

### 65 Input and Output Redirects

-   There are 3 redirects in Linux
    		1\. Standard input (**stdin**) and it has file descriptor number as 0
    		2\. Standard output (**stdout**) and it has file descriptor number as 1
    		3\. Standard error (**stderr**) and it has file descriptor number as 2

#### Output

-   Output (**stdout**) - 1
    -   By default when running a command it's output goes to the terminal.
    -   The output of a command can be routed to a file using `>` symbol.
        -   E.g. `ls -l > listings`
        -   E.g. `pwd \> findpath`
    -   If using the same file for additional output or to append to the same file then use `>>`
        -   E.g. `ls -la >> listings`
        -   E.g. `echo 'Hello World' >> findpath`

**Terminal Example**

```bash
~ $ pwd
/home/tklein
~ $ ls -la > homedirlisting
# Shows the listing of the home directory
# and overwrites any existing content of the file.
~ $ cat homedirlisting
# Append to the previous input
~ $ ls -ltr >> homedirlisting
# cat 'homedirlisting' again to verify it was appended.
~ $ cat homedirlisting
# Overwriting what was previously written
# to the file 'homedirlisting'
~ $ echo 'Christmas is around the corner.' > homedirlisting
~ $ cat homedirlisting
Christmas is around the corner.
~ $
```

#### Input

-   Input (**stdin**) - 0
    -   Input is used when feeding file contents to a file.
    -   E.g. `cat < listings` - cat takes listings as input.
    -   E.g. `mail -s 'Office memo' allusers@bestmail.com < memoletter`

#### Error

-   Error (**stderr**) - 2
    		\- When a command is executed we use a keyboard and that is also considered (**stdin - 0**)
    		\- That command ouput goes on the monitor and that output is (**stdout -  1**)
    		\- If the command produced any error on the screen then it is considered (**stderr - 2**)
    			\- We can use redirects to route errors from the screen.
    				\- E.g. `ls -l /root 2> errorfile`
    				\- E.g. `telnet localhost 2> errorfile`

**Terminal Example**

```bash
# The following command gives errors as output.
~ $ telnet localhost
Trying ::1...
telnet: connect to address ::1: Connection refused
Trying 127.0.0.1...
telnet: connect to address 127.0.0.1: Connection refused
# These two errors qualify as 'stderr - 2' and so can be
# redirected to any textfile and will not appear on screen,
# if redirected.
~ $ telnet localhost 2> errorfile
Trying ::1...
Trying 127.0.0.1...
~ $ cat errorfile
telnet: connect to address ::1: Connection refused
telnet: connect to address 127.0.0.1: Connection refused
~ $
```

### 66 Standard Output to a File (`tee`)

-   `tee` command is used to store and view (both at the same time) the output of any command.
-   The command is named after the T-splitter used in plumbing. It basically breaks the output of a program so that it can be both displayed on screen and saved in a file. It does both simultaneously. It copies the result into the specified files or variabless and also display the result.

#### Terminal Example

```bash
~ $ echo 'Christmas only happens once a year.' | tee christmas_truths
Christmas only happens once a year.
~ $ cat christmas_truths
Christmas only happens once a year.
~ $ rm christmas_truths
~ $ echo 'Christmas only happens once a year.' | tee christmas_truths
Christmas only happens once a year.
~ $ cat christmas_truths
Christmas only happens once a year.
# The tee command replaces existing text already present in the file,
# if used without an option.
~ $ echo 'Christmas only happens once a year. We believe so.' | tee christmas_truths
Christmas only happens once a year. We believe so.
~ $ cat christmas_truths
Christmas only happens once a year. We believe so.
# Using option `-a` the text gets appended instead.
~ $ echo 'Christmas only happens once a year.' | tee -a christmas_truths
Christmas only happens once a year.
~ $ cat christmas_truths
Christmas only happens once a year. We believe so.
Christmas only happens once a year.
```


```bash
# text input can be redirected to multiple files at once.
# These files do not have to exist prior to running the
# command `tee`.
~ $ ls -l | tee file1 file2 file3
```

**Misc.**
- The version of a command can be looked up by entering the command:
- `<command> --version`


```sh
~ $ tee --version
tee (GNU coreutils) 8.22
Copyright (C) 2013 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Written by Mike Parker, Richard M. Stallman, and David MacKenzie.
~ $
```

-    The word count in a text file can be looked up by using command
-   `wc -c [file]`

```bash
~ $ wc -c christmas_truths
87 christmas_truths
```

### 67 Pipes `|`

-   A pipe is used by the shell to connect the ouput of one command directly to the input of another command.
-   The symbol for a pipe is the vertical bar `|`.
-   The structure of a pipe command looks like this:
    -   `command1 [arguments] | command2 [arguments]`
    -   E.g. `ls -l | <command2> [arguments]`

### 68 File Maintainance Commands

\(`cp`,`rm`,`mv`,`mkdir`,`rmdir`)

#### cp

-   `cp`
    -   Copies files and directories.
    -   Basic structure of the command is among others:
        `cp [OPTION] <SOURCE> <DEST>`
    -   If one wants to copy an entire directory to another one, the `-R` or `-r` option has to be included in the command for it to copy the source directory recursively to the destination directory.

#### rm

-   `rm`
    -   Lets the user remove (delete) files or directories.
    -   The command is destructive and must be used with great care, especially when using the following options:
        -   `-f` or `--force` never prompts the user before something is removed.
        -   `-r`, `-R` or `--recursive` removes directories and their contents recursively.
        -   Any combination of the above commands, including none of them together with wildcards.
    -   The command has several options that can act as a safety net, so the user gets prompts, warnings or more control over how verbose the command is once executed. This can reduce the danger of involuntarily removing essential files and directories of the system. See `man rm` for details.

#### mv

-   `mv`
-   moves or renames files.
-   `mv [OPTION]... [-T] <SOURCE> <DEST>`
    -   With `-T`, it treats the `DEST` as a regular file and not as a 	directory.
    -   It renames `SOURCE` to `DEST`

##### `mv -T`

An Example that also shows that it works without using `-T` as well.
As illustrated below. One just can't specify a directory as `DEST` for it to work.
It also shows that only the file name gets changed, the content of the original file remains the same:

```bash
~ $ ls -ltr david*
-r--r--r--. 1 tklein tklein 0 De20 06:21 david
~ $ echo "This fildocuments the endevour of findindavid's last name" > david
-bash: david: Permission denied
~ $ su
Password:
root $ chmod 771 david
root $ ls -ltr david
-rwxrwx--x. 1 tklein tklein 0 De20 06:21 david
root $ exit
exit
```

```bash
~ $ whoami
tklein
~ $ echo "This fildocuments the endevour of findindavid's last name" > david
~ $ cat david
This file documents the endevour ofinding david's last name
~ $ cp david david_2
~ $ mv -T davidavid_hasselhof
~ $ cadavid_hasselhof
This file documents the endevour ofinding david's last name
~ $ mv david_2 david
~ $ rm david_hasselhof
~ $ mv davidavid_hasselhoff
~ $ cadavid_hasselhoff
This file documents the endevour ofinding david's last name
~ $
```

##### mv

-   `mv [OPTION]... <SOURCE...> <DIRECTORY>`
-   Like this, it moves `SOURCE` to `DIRECTORY`

###### Example

```bash
~ $ ls -ltr
total 9284
...
drwxrwxr-x. 2 tklein tklein      67 Dec 20 13:00 seinfeld
drwxrwxr-x. 2 tklein tklein      67 Dec 20 13:02 seinfelds_backup_plan
-rw-rw-r--. 1 tklein tklein       0 Dec 20 22:25 seinfelds_secret_plan
~ $ mv seinfelds_secret_plan seinfeld
~ $ ls -ltr seinfeld
total 0
-rw-rw-r--. 1 tklein tklein 0 Dec 20 12:58 seinfelds_fave_file
-rw-rw-r--. 1 tklein tklein 0 Dec 20 12:59 seinfelds_second_fave_file
-rw-rw-r--. 1 tklein tklein 0 Dec 20 22:25 seinfelds_secret_plan
~ $
```

#### mkdir

-   `mkdir [OPTION]... <DIRECTORY>...`
    -   Creates the  DIRECTORY\(ies), if they do not already exist.
    -   OPTION `-p`
  		- gives no error, if existing.
  		- Creates parent directories as needed.

To understand better what the difference between using `mkdir` without the `-p` option and using it with the `-p` option, here is an example\:

##### Using `mkdir <DIRECTORY>`

In the current directory there is a directory called 'seinfeld' at the bottom of the `ls -ltr` command\:

```bash
~ $ ls -ltr
total 4
-rw-rw-r--. 1 tklein tklein    0 Dec 23 13:26 special_reward
-rw-rw-r--. 1 tklein tklein    0 Dec 23 13:26 pamela-anderson
-rw-rw-r--. 1 tklein tklein    0 Dec 23 13:26 david-hasselhoff
-rw-rw-r--. 1 tklein tklein    0 Dec 23 13:26 check
drwxrwxr-x. 2 tklein tklein    6 Dec 23 13:27 morganas_secrets
drwxrwxr-x. 2 tklein tklein    6 Dec 23 13:27 donald_duck
drwxrwxr-x. 2 tklein tklein    6 Dec 23 13:28 david-hasselhoffs-mansion
drwxrwxr-x. 2 tklein tklein 4096 Dec 23 13:32 cars
-rw-rw-r--. 1 tklein tklein    0 Dec 23 13:47 david
drwxrwxr-x. 3 tklein tklein   28 Dec 23 14:03 seinfeld
```

If one tries to create a directory called 'seinfeld' in the current directory using `mkdir seinfeld`, one gets an error that it already exists and it was not created\:

```bash
~ $ mkdir seinfeld
mkdir: cannot create directory 'seinfeld': File exists
~ $ ls -ltr
total 4
...
drwxrwxr-x. 3 tklein tklein   28 Dec 23 14:03 seinfeld
```

The time of creation is exactly the same as before and so the old file was not overwritten.

##### Using `mkdir -p <DIRECTORY>`

```bash
~ $ mkdir -p seinfeld
~ $ ls -ltr
total 4
...
drwxrwxr-x. 3 tklein tklein   28 Dec 23 14:03 seinfeld
```

No error message and the original file was not overwritten.
In both cases `mkdir` only creates a new directory, if no existing one would be overwritten by executing the command.

There is another use case for the `-p` option. One reads in `mkdir --help`\:

> \-p, --parents     no error if existing, make parent directories as needed

So, if one wanted to create a nested folder in a folder that does not yet exist, without the `-p` option one would have to type something like the following to make that happen. Here the aim is to create a folder called 'introduction' inside a non-existing folder called 'the_great_adventure'.

###### Example\:

```bash
~ $ mkdir the_great_adventure/introduction
mkdir: cannot create directory 'the_great_adventure/introduction': No such file or directory
```

Using the `-p` option, one can create all necessary parent directories and the final directory in the new hierarchy like so\:

```bash
~ $ mkdir the_great_adventure/introduction
mkdir: cannot create directory 'the_great_adventure/introduction': No such file or directory

~ $ mkdir -p the_great_adventure/introduction
~ $ ls -ltr
total 4
...
~ $ ls -ltr the_great_adventure/
total 0
drwxrwxr-x. 2 tklein tklein 6 Dec 23 14:52 introduction
~ $
```

#### rmdir

`rmdir [OPTIONS] <DIRECTORY>`

Looking into `rmdir --help` one gets the following information about what the command does\:

>     Remove the DIRECTORY(ies), if they are empty.

-    The command will fail, if a directory is not empty. There can be hidden files in the directory for example that can only be seen using `ls -a /path/to/dir/` the `-a` option shows all files in a directory.

##### `rmdir --ignore-fail-on-non-empty <DIRECTORY>`

-   With the option `--ignore-fail-on-non-empty` non empty directories can be deleted.

##### `rmdir -p <DIRECTORY1/2/3`

-   With this option directories can be removed recursively. See example.

```bash
~ $ mkdir -p first_dir/second_dir/third_dir
~ $ rmdir first_dir/
rmdir: failed to remove 'first_dir/': Directory not empty
~ $ rmdir -p first_dir/second_dir/third_dir
~ $ ls -ltr
total 4
-rw-rw-r--. 1 tklein tklein    0 Dec 23 13:26 special_reward
-rw-rw-r--. 1 tklein tklein    0 Dec 23 13:26 pamela-anderson
-rw-rw-r--. 1 tklein tklein    0 Dec 23 13:26 david-hasselhoff
-rw-rw-r--. 1 tklein tklein    0 Dec 23 13:26 check
drwxrwxr-x. 2 tklein tklein    6 Dec 23 13:27 morganas_secrets
drwxrwxr-x. 2 tklein tklein    6 Dec 23 13:27 donald_duck
drwxrwxr-x. 2 tklein tklein    6 Dec 23 13:28 david-hasselhoffs-mansion
drwxrwxr-x. 2 tklein tklein 4096 Dec 23 13:32 cars
-rw-rw-r--. 1 tklein tklein    0 Dec 23 13:47 david
drwxrwxr-x. 3 tklein tklein   28 Dec 23 14:03 seinfeld
drwxrwxr-x. 3 tklein tklein   26 Dec 23 14:52 the_great_adventure
```

#### chown and chgrp

For both commands one needs admin rights / needs to be root to use them.

##### chown

-   `chown` from the `chown --help` command, one learns\:

> Change the owner and/or group of each FILE to OWNER and/or GROUP.
> With --reference, change the owner and group of each FILE to those of RFILE.

and:

1.  Usage: chown [OPTION]... [OWNER]&#x3A;[GROUP]] FILE...

2.  or:  chown [OPTION]... --reference=RFILE FILE...

One can change the owner or group or owner and group together using 1.
An example of this behavior:

A file is owned by user root and belongs to group root.

```bash
root $ ls -ltr
total 0
-rw-r--r--. 1 root root 0 Dec 23 19:43 bruce_lee_knows
```

Being root, one can change owner and group together like so\:

_One can change owner or group alone, by only entering what is written directly before the colon **\:** and what is right after the **\:** to change the group. Without the colon._

```bash
root $ chown tklein:tklein bruce_lee_knows
```

Checking owner and group after using the command, verifies that both changed to 'tklein'

```bash
root $ ls -ltr
total 0
-rw-r--r--. 1 tklein tklein 0 Dec 23 19:43 bruce_lee_knows
root $
```

###### chown \[-R]

With the `-R` option one can change ownership and or group recursively for several nested directories.

###### chown \[OP] --reference=RFILE FILE...

This is case 2. from above. Here one can use another file's owner and or group as a reference and apply it to the file or directory. Options like `-R` can still be used.

<h6>Example</h6>

```bash
root $ ls -ltr
total 0
-rw-r--r--. 1 tklein tklein 0 Dec 23 19:43 bruce_lee_knows
-rw-r--r--. 1 root   root   0 Dec 23 19:57 bruce_lee_chronicles
root $ chown --reference=bruce_lee_knows bruce_lee_chronicles
root $ ls -ltr
total 0
-rw-r--r--. 1 tklein tklein 0 Dec 23 19:43 bruce_lee_knows
-rw-r--r--. 1 tklein tklein 0 Dec 23 19:57 bruce_lee_chronicles
root $
```

<h5>chgrp</h5>

Using the help function, one gets the information\:

> Usage: chgrp [OPTION]... GROUP FILE...
>   or:  chgrp [OPTION]... --reference=RFILE FILE...
> Change the group of each FILE to GROUP.
> With --reference, change the group of each FILE to that of RFILE.

###### Example

```bash
root $ ls -ltr
total 0
-rw-r--r--. 1 tklein tklein 0 Dec 23 19:43 bruce_lee_knows
-rw-r--r--. 1 tklein tklein 0 Dec 23 19:57 bruce_lee_chronicles
root $ chgrp root bruce_lee_knows
root $ ls -ltr
total 0
-rw-r--r--. 1 tklein root   0 Dec 23 19:43 bruce_lee_knows
-rw-r--r--. 1 tklein tklein 0 Dec 23 19:57 bruce_lee_chronicles
```

### File Display Commands

Commands that are used to display the contents of a file.

#### cat

gives you the entire file in the output. One needs to scroll, if the file has more lines than can be displayed at once in the terminal window.

###### Example

There is a large text file 'messages' in this example that has 2118 lines. Using `cat messages` will output all lines at once into the terminal window, which is often unpractical.

```bash
root $ wc -l messages
2118 messages
```

#### more

Using `more messages` one gets one page at a time as output and it is easy to move down the file like that by using the 'space bar'. Moving down is the only thing one can do with this command however, as stated in the man pages of `less`. See below. To get out of the output `more <file>` produces, one presses `q`

#### less

Less is a similar command to `more`, but with some key differences. From `man less`\:

> Less is a program similar to more (1), but which allows backward movement in the file as well as for-
>        ward movement.  Also, less does not have to read the entire input file before starting, so with large
>        input  files  it  starts  up faster than text editors like vi (1). ...

Using the keyboard, one can move down (line for line), by pressing `k` once per line and up by pressing `j` in the same manner. Exiting the output can be done by pressing `q`.

#### head

`head [OPTION]... [FILE]...`

-   By default it prints the first 10 lines of a file, if no options are used.
-   If given more than one file, it shows the specified (or default) number of lines for both files. See the example.
-   If no FILE is specified or if FILE is `-`, it reads from standard input.

###### Example

```bash
root $ head -4 messages_head50 messages_tail30
==> messages_head50 <==
Dec 23 13:16:58 localhost journal: Runtime journal is using 6.1M (max allowed 48.9M, trying to leave 73.3M free of 483.1M available → current limit 48.9M).
Dec 23 13:16:58 localhost kernel: Initializing cgroup subsys cpuset
Dec 23 13:1
<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->
6:58 localhost kernel: Initializing cgroup subsys cpu
Dec 23 13:16:58 localhost kernel: Initializing cgroup subsys cpuacct

==> messages_tail30 <==
Dec 23 20:39:46 localhost systemd: Starting Network Manager Script Dispatcher Service...
Dec 23 20:39:46 localhost dhclient[31642]: bound to 192.168.178.101 -- renewal in 351362 seconds.
Dec 23 20:39:46 localhost dbus[688]: [system] Successfully activated service 'org.freedesktop.nm_dispatcher'
Dec 23 20:39:46 localhost systemd: Started Network Manager Script Dispatcher Service.
root $
```

TODO Check if your usage of &lt;...> and [...] in the command blue prints is correct for each command.

#### tail

`tail [OPTION]... [FILE]...`

### Filters / Text Processing Commands (Overview)

The following commands will be described in the following\:

-   `cut`
-   `awk`
-   `grep` and `egrep`
-   `sort`
-   `uniq`
-   `wc`

### cut - Text Processor Commands

`cut <OPTION>... [FILE]...`

Cut is a command line utility, that allows you to cut parts of lines from specified files or piped data and print the result to standard output. It can be used to cut parts of a line by\:

-   delimiter
-   byte position
-   character

#### cut filename

Does not work! See `man cut` or `cut --help`

#### cut --version

#### cut -c\[n] filename

-   With \[n] being a  positive integer.
-   Prints out the n-th character on each line.
    		\- cut -c1,2,4

```bash
~ $ cut -c1,2,4 overview
cop
cov
cop
crs
muc
ofr
sea
sho
spr
stt
sue
su-
va-
vit
~ $
```

```bash
~ $ cut -c1-4 overview
comp
conv
coup
cros
musc
offr
seda
shoo
spor
stat
supe
suv-
van-
vint
~ $
```

```bash
~ $ cut -c1-3,6-8 overview
comct-
conrti
cou-ca
cro-ov
muse-c
offad-
sed-ca
shoing
spos-c
staon_
sup-ca
suvate
vanate
vinge-
~ $
```

Bytes can give different results compared to lines.

```bash
~ $ cut -b1-3 overview
com
con
cou
cro
mus
off
sed
sho
spo
sta
sup
suv
van
vin
~ $
```

##### For csv like files

-   List the first 6 columns separated by ':'
-   The fiile `/etc/passwd` has user information stored in it.

```bash
~ $ cut -d: -f 6 /etc/passwd
/root
/bin
/sbin
/var/adm
/var/spool/lpd
/sbin
/sbin
/sbin
/var/spool/mail
/root
/usr/games
/var/ftp
/
/
/
/
/var/run/lsm
/var/lib/rpcbind
/etc/abrt
/dev/null
/run/gluster
/var/lib/nfs
/var/lib/nfs
/var/lib/pcp
/var/empty/sshd
/var/spool/postfix
/var/lib/chrony
/etc/ntp
/var/lib/oprofile
/
/home/tklein
~ $
```

```bash
~ $ cut -d: -f 6-7 /etc/passwd
/root:/bin/bash
/bin:/sbin/nologin
/sbin:/sbin/nologin
/var/adm:/sbin/nologin
/var/spool/lpd:/sbin/nologin
/sbin:/bin/sync
/sbin:/sbin/shutdown
/sbin:/sbin/halt
/var/spool/mail:/sbin/nologin
/root:/sbin/nologin
/usr/games:/sbin/nologin
/var/ftp:/sbin/nologin
/:/sbin/nologin
/:/sbin/nologin
/:/sbin/nologin
/:/sbin/nologin
/var/run/lsm:/sbin/nologin
/var/lib/rpcbind:/sbin/nologin
/etc/abrt:/sbin/nologin
/dev/null:/sbin/nologin
/run/gluster:/sbin/nologin
/var/lib/nfs:/sbin/nologin
/var/lib/nfs:/sbin/nologin
/var/lib/pcp:/sbin/nologin
/var/empty/sshd:/sbin/nologin
/var/spool/postfix:/sbin/nologin
/var/lib/chrony:/sbin/nologin
/etc/ntp:/sbin/nologin
/var/lib/oprofile:/sbin/nologin
/:/sbin/nologin
/home/tklein:/bin/bash
~ $
```

```bash
~ $ ls -l | cut -c2-4
ota
rw-
rw-
rw-
rw-
rw-
rw-
rw-
rw-
rw-
rw-
rw-
rw-
rw-
rw-
rw-
rw-
~ $
```

### awk - Text Processors Commands

`awk` is a utility \\/ language designed for data extraction. Most of the time it is used to extract fields from a file or from an output.

```bash
~ $ awk --version
GNU Awk 4.0.2
Copyright (C) 1989, 1991-2012 Free Software Foundation.

This program is free software; you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation; either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program. If not, see http://www.gnu.org/licenses/.
~ $
```

Here a pipe was used to limit the lines, that the output generates for readability. Without the pipe, using the command on the entire file, it would look like this\:

`awk -F , '{print $1}' cars.csv`

-   `-F` option tells it, that the delimiter in this file is comma. For 'space' nothing has to be specified as an option.

```bash
~ $ head -5 cars.csv | awk -F , '{print $1}' -
""
"1"
"2"
"3"
"4"
~ $
```

-   Specifying `$NF` in the print statement, prints the last column in the data set.

```bash
~ $ head -5 cars.csv | awk -F , '{print $NF}' -
"dist"
2
10
4
22
```

-   In the example below, only the row is printed from the data set, where the word 'dist' is matched. It is part of the header, so row / line No. 1 gets printed.

```bash
~ $ awk '/dist/ {print}' cars.csv
"","speed","dist"
~ $
```

-   Using a pipe, below the example changes the second column (`$2`) from 'Jess' to 'Adam' and afterwards prints, according to the following table\:

|    Input   |       Output      |
| :--------: | :---------------: |
| `print $0` | Print all columns |
| `print $1` |   Print column 1  |
| `print $2` |   Print column 2  |

```bash
~ $ echo "Hello Jess" | awk '{$2="Adam" ; print $0}'
Hello Adam
~ $ echo "Hello Jess" | awk '{$2="Adam" ; print $1}'
Hello
~ $ echo "Hello Jess" | awk '{$2="Adam" ; print $2}'
Adam
~ $
```

Replacing the entries in the third column 'dist' with 'NAN'. This could be necessary, if the values in the 'dist' column were not valid and one had to clean the 'dist' column.

```bash
~ $ head -5 cars.csv | awk -F , '{$3="NAN" ; print $0}'
"" "speed" NAN
"1" 4 NAN
"2" 4 NAN
"3" 7 NAN
"4" 7 NAN
~ $
```

```bash
~ $ awk 'length($0) > 15' cars.csv
"","speed","dist"
~ $
```

Print the line, where the entry in column 9 is "overview"

```bash
~ $ ls -l | awk '{if($9 == "overview") print $0;}'
-rw-rw-r--. 1 tklein tklein 242 Dec 24 00:26 overview
~ $ ls -l
total 20
-rw-rw-r--. 1 tklein tklein 298 Dec 24 01:13 ,
-rw-rw-r--. 1 tklein tklein 552 Dec 24 01:50 cars.csv
-rw-rw-r--. 1 tklein tklein 552 Dec 24 01:44 cars_backup.csv
-rw-rw-r--. 1 tklein tklein   0 Dec 23 13:30 compact-category
-rw-rw-r--. 1 tklein tklein   0 Dec 23 13:30 convertible-category
-rw-rw-r--. 1 tklein tklein   0 Dec 23 13:32 coupe-category
-rw-rw-r--. 1 tklein tklein   0 Dec 23 13:32 cross-over-category
-rw-rw-r--. 1 tklein tklein   0 Dec 23 13:30 muscle-category
-rw-rw-r--. 1 tklein tklein   0 Dec 23 13:32 offroad-category
-rw-rw-r--. 1 tklein tklein 242 Dec 24 00:26 overview
-rw-rw-r--. 1 tklein tklein 242 Dec 24 00:28 overview_backup
-rw-rw-r--. 1 tklein tklein   0 Dec 23 13:32 sedan-category
-rw-rw-r--. 1 tklein tklein   0 Dec 23 13:32 shooting_break-category
-rw-rw-r--. 1 tklein tklein   0 Dec 23 13:30 sports-category
-rw-rw-r--. 1 tklein tklein   0 Dec 23 13:32 station_wagon-category
-rw-rw-r--. 1 tklein tklein   0 Dec 23 13:32 super-category
-rw-rw-r--. 1 tklein tklein   0 Dec 23 13:32 suv-category
-rw-rw-r--. 1 tklein tklein   0 Dec 23 13:32 van-category
-rw-rw-r--. 1 tklein tklein   0 Dec 23 13:32 vintage-category
```

Number of fields

```bash
~ $ ls -l | awk '{print NF}'
2
9
9
9
9
9
9
9
9
9
9
9
9
9
9
9
9
9
9
9
~ $
```

### grep/egrep - Text Processor Commands

-   What is grep?
    -   The grep command which stands for "global regular expressions print", processes text line by line and prints any lines which match a specified pattern.

#### Specific grep / egrep commands

##### grep --version

Check version of grep

##### grep --help

Get a shorter summary of what the command does with it\\'s  options and basic structure.

##### man grep

Get detailed information about the command. Similiar to `grep --help`, but with more details often. The difference between `man <command>` and `<command> --help` varies by command.

##### grep keyword file

```bash
~ $ grep "Sport" cars/suv-category
SUV = Sport Utility Vehicle
~ $
```

##### grep -c keyword file

Counts the matches in the file.

```bash
~ $ grep -c "Sport" cars/suv-category
1
~ $
```

##### grep -i keyword file

Without the `-i` option, it is case-sensitive and with it, it is not. See example below.

```bash
~ $ echo -e '"SUV = Sport Utility Vehicle" A vehicle in this class ususally is not sporty on average.' > cars/suv-category
~ $ cat cars/suv-category
"SUV = Sport Utility Vehicle" A vehicle in this class ususally is not sporty on average.
~ $ grep 'Sport' cars/suv-category
"SUV = Sport Utility Vehicle" A vehicle in this class ususally is not sporty on average.
~ $ grep 'sport' cars/suv-category
"SUV = Sport Utility Vehicle" A vehicle in this class ususally is not sporty on average.
~ $ grep -i 'Sport' cars/suv-category
"SUV = Sport Utility Vehicle" A vehicle in this class ususally is not sporty on average.
~ $
```

##### grep -n keyword file

Prints the line number for each match, as well.

```bash
~ $ grep -n sport cars/suv-category
1:"SUV = Sport Utility Vehicle" A vehicle in this class ususally is not sporty on average.
```

##### grep -v keyword file

grep will match anything in the file, except the keyword that is entered.

###### Example

A file with 6 lines is used.

```bash
~ $ wc -l cars/suv-category
6 cars/suv-category
~ $
```

the term 'sport' is **not** found on lines 1,3,4. There are only matches on line 2 and 6, that are not printed in the output.

```bash
~ $ grep -vn sport cars/suv-category
1:
3:
4:There is no commonly agreed-upon definition of an SUV, and usage of the term varies between countries.
~ $
```

##### grep keyword file | awk '{print $1}'

Search for a keyword and then only give the 1st. field.
Here, entry '"41"' is found in the first column on line 6 of the last 15 lines of file 'cars.csv' and the line is omitted in the output, as shown by the line numbers on the very left of the output, E.g. '1:'.
Only the first column, that gives the row index for each entry in the dataset is returned where '"41"' is not an entry.

```bash
~ $ tail -15 cars/cars.csv | grep -vn "\"41\"" - | awk -F , '{print $1}'
1:"36"
2:"37"
3:"38"
4:"39"
5:"40"
7:"42"
8:"43"
9:"44"
10:"45"
11:"46"
12:"47"
13:"48"
14:"49"
15:"50"
~ $
```

A sample line in file 'overview', that is used in the following:

```bash
~ $ head -1 overview
compact-category
~ $
```

-   `grep` matches case sensitively all lines that do not contain 'sedan' in the file 'overview'.
-   Using `awk`, only the part before custom separator '-' is printed.
-   `cut` prints characters 1 to 3 of what was is the output of
    `awk -F - '{print $1}'`

```bash
~ $ grep -vi sedan overview | awk -F - '{print $1}' | cut -c1-3
com
con
cou
cro
mus
off
sho
spo
sta
sup
suv
van
vin
~ $
```

Below is the output of command `ls -l`, as ran in my user accounts home directory. Notice, that any file that contains 'messages\*' is written in lowercase.

```bash
~ $ ls -l
total 208
-rwxr-xr-x. 1 tklein tklein   5137 Dec 24 06:05 Film.csv
-rw-rw-r--. 1 tklein tklein   1144 Dec 24 03:23 ]
drwxrwxr-x. 2 tklein tklein   4096 Dec 24 03:24 cars
-rw-rw-r--. 1 tklein tklein      0 Dec 23 13:26 check
-rw-rw-r--. 1 tklein tklein      0 Dec 23 13:47 david
-rw-rw-r--. 1 tklein tklein      0 Dec 23 13:26 david-hasselhoff
drwxrwxr-x. 2 tklein tklein      6 Dec 23 13:28 david-hasselhoffs-mansion
drwxr-xr-x. 2 root   root       57 Dec 23 19:57 display_chown
drwxrwxr-x. 2 tklein tklein      6 Dec 23 13:27 donald_duck
drwxrwxr-x. 2 tklein tklein     22 Dec 24 06:06 film
-rw-------. 1 root   root   183192 Dec 23 21:46 messages
-rw-r--r--. 1 root   root     5565 Dec 23 21:53 messages_head50
-rw-r--r--. 1 root   root     2233 Dec 23 23:00 messages_tail30
drwxrwxr-x. 2 tklein tklein      6 Dec 23 13:27 morganas_secrets
-rw-rw-r--. 1 tklein tklein      0 Dec 23 13:26 pamela-anderson
drwxrwxr-x. 3 tklein tklein     28 Dec 23 14:03 seinfeld
-rw-rw-r--. 1 tklein tklein      0 Dec 23 13:26 special_reward
drwxrwxr-x. 3 tklein tklein     26 Dec 23 14:52 the_great_adventure
```

Specifying the `-i` option in the `grep` command, it matches non case sensitively and one gets all the 'message\*' entries in the directory.

```bash
~ $ ls -l | grep -i Message
-rw-------. 1 root   root   183192 Dec 23 21:46 messages
-rw-r--r--. 1 root   root     5565 Dec 23 21:53 messages_head50
-rw-r--r--. 1 root   root     2233 Dec 23 23:00 messages_tail30
~ $
```

#### egrep

##### egrep -i "keyword|keyword2" file

The command matches all occurences of 'compact' and 'super' in the specified file 'overview'.

```bash
~ $ egrep -i "compact|super" cars/overview
compact-category
super-category
~ $
```

### sort/uniq - Text Processor Commands

-   `sort` command sorts in alphabetical order.
-   `uniq` filters out the repeated or duplicate lines.

#### Informational Commands

-   `sort --version`
-   `man sort`
-   `sort --help`

#### sort - default behavior

Running `sort` with no options on a file, gives the following output\:

```bash
# The lines are sorted alphabetically,
# in ascending order.
~ $ sort cars/overview
compact-category
convertible-category
coupe-category
cross-over-category
electrical-category
muscle-category
offroad-category
sedan-category
shooting_break-category
sports-category
station_wagon-category
super-category
suv-category
van-category
vintage-category
```

Sorting alphabetically, in descending order can be done like so\:

```bash
~ $ sort -r cars/overview
vintage-category
van-category
suv-category
super-category
station_wagon-category
sports-category
shooting_break-category
sedan-category
offroad-category
muscle-category
electrical-category
cross-over-category
coupe-category
convertible-category
compact-category
```

By default, `sort` starts sorting from the beginning of the first row. One can change this behavior, by specifying the column, that should be used by `sort` to create a sorted output. That includes the option to give `sort` a separator, that is other than whitespace. See example, below, where the file was sorted by whatever comes after the '-' sign\:

```bash
~ $ sort -k2 -t- cars/overview
compact-category
convertible-category
coupe-category
electrical-category
muscle-category
offroad-category
sedan-category
shooting_break-category
sports-category
station_wagon-category
super-category
suv-category
van-category
vintage-category
cross-over-category
~ $
```

Sorting by the $last == 9th$ column of the command `ls -l`\:

```bash
~ $ ls -l | sort -k9
total 208
-rwxr-xr-x. 1 tklein tklein   5137 Dec 24 06:05 Film.csv
-rw-rw-r--. 1 tklein tklein   1144 Dec 24 03:23 ]
drwxrwxr-x. 2 tklein tklein   4096 Dec 24 06:46 cars
-rw-rw-r--. 1 tklein tklein      0 Dec 23 13:26 check
-rw-rw-r--. 1 tklein tklein      0 Dec 23 13:47 david
-rw-rw-r--. 1 tklein tklein      0 Dec 23 13:26 david-hasselhoff
drwxrwxr-x. 2 tklein tklein      6 Dec 23 13:28 david-hasselhoffs-mansion
drwxr-xr-x. 2 root   root       57 Dec 23 19:57 display_chown
drwxrwxr-x. 2 tklein tklein      6 Dec 23 13:27 donald_duck
drwxrwxr-x. 2 tklein tklein     22 Dec 24 06:06 film
-rw-------. 1 root   root   183192 Dec 23 21:46 messages
-rw-r--r--. 1 root   root     5565 Dec 23 21:53 messages_head50
-rw-r--r--. 1 root   root     2233 Dec 23 23:00 messages_tail30
drwxrwxr-x. 2 tklein tklein      6 Dec 23 13:27 morganas_secrets
-rw-rw-r--. 1 tklein tklein      0 Dec 23 13:26 pamela-anderson
drwxrwxr-x. 3 tklein tklein     28 Dec 23 14:03 seinfeld
-rw-rw-r--. 1 tklein tklein      0 Dec 23 13:26 special_reward
drwxrwxr-x. 3 tklein tklein     26 Dec 23 14:52 the_great_adventure
```

#### Uniq file

One duplicate line, 'coupe-category' in the text file.

```bash
~ $ sort cars/overview
compact-category
convertible-category
coupe-category
coupe-category # duplicate
cross-over-category
electrical-category
muscle-category
offroad-category
sedan-category
shooting_break-category
sports-category
station_wagon-category
super-category
suv-category
van-category
vintage-category
~ $
```

One should always run `uniq` with the piped output of sort, like in the example below\:

```bash
~ $ sort cars/overview | uniq
compact-category
convertible-category
coupe-category
cross-over-category
electrical-category
muscle-category
offroad-category
sedan-category
shooting_break-category
sports-category
station_wagon-category
super-category
suv-category
van-category
vintage-category
~ $
```

Using `-c` option, the output tells the user how often each line is repeated in the file. Here, only 'coupe-category' has to entries and so is the only line to have a '2' associated with it.

```bash
~ $ sort cars/overview | uniq -c
      1 compact-category
      1 convertible-category
      2 coupe-category
      1 cross-over-category
      1 electrical-category
      1 muscle-category
      1 offroad-category
      1 sedan-category
      1 shooting_break-category
      1 sports-category
      1 station_wagon-category
      1 super-category
      1 suv-category
      1 van-category
      1 vintage-category
~ $
```

Only lines with duplicates as displayed.

```bash
~ $ sort cars/overview | uniq -d
coupe-category
~ $
```

### wc - Text Processor Commands

-   `wc` stands for 'word count'.
-   It can read from the following\:
    -   standard input
    -   list of files
-   It can generate\:
    -   new line count
    -   word count
    -   byte count

#### Informational Commands

-   `wc --version`
-   `wc --help`
-   `man wc`

#### wc file

-   The output reads from left to right, as follows with the number from the example in braces:
    -   Number of lines in the file (16).
    -   Number of words in the file (16).
    -   Number of bytes in the file (277).

```bash
~ $ wc cars/overview
 16  16 277 cars/overview
~ $
```

If one only wants to have the number of lines printed\:

```bash
~ $ wc -l cars/overview
16 cars/overview
~ $
```

If one only wants to have the number of words printed\:

```bash
~ $ wc -w cars/overview
16 cars/overview
~ $
```

If one only wants to have the number of bytes printed\:

```bash
~ $ wc -c cars/overview
277 cars/overview
~ $
```

The number of the following command includes the first line of the `ls -ltr` output, which is neither a directory, nor is it a file. The actual number of objects in the current directory, in the example is $19-1=18$.

```bash
~ $ ls -ltr | wc -l
19
~ $
```

#### ls -d \*\/

##### Directories located in the current directory

If one only wants the directories printed, that are in the current directory using `ls`, there is a way to do so.
If one wants the directories in the current directory listed, the following will do so\:

It uses `ls -d`, with `-d` printing not the contents of any directory, but printing the name of the directory instead. the wildcard `*` plus `/` tells `ls` to only print such objects in the current directory, that are directories themselves. Any directory ends with a `/` sign at the end of it\\'s `ls -ld` output.

```bash
~ $ ls -ld */
drwxrwxr-x. 2 tklein tklein 4096 Dec 24 07:41 cars/
drwxrwxr-x. 2 tklein tklein    6 Dec 23 13:28 david-hasselhoffs-mansion/
drwxr-xr-x. 2 root   root     57 Dec 23 19:57 display_chown/
drwxrwxr-x. 2 tklein tklein    6 Dec 23 13:27 donald_duck/
drwxrwxr-x. 2 tklein tklein   22 Dec 24 06:06 film/
drwxrwxr-x. 2 tklein tklein    6 Dec 23 13:27 morganas_secrets/
drwxrwxr-x. 3 tklein tklein   28 Dec 23 14:03 seinfeld/
drwxrwxr-x. 3 tklein tklein   26 Dec 23 14:52 the_great_adventure/
~ $
```

##### Any directory using the absolute path

To print the sub-directories of any directory using it\\'s absolute path in combination with `ls -ld`, one can do so in a similiar fashion, as for the 'current directory' example\:

```bash
~ $ ls -ld /home/tklein/*/
drwxrwxr-x. 2 tklein tklein 4096 Dec 24 07:41 /home/tklein/cars/
drwxrwxr-x. 2 tklein tklein    6 Dec 23 13:28 /home/tklein/david-hasselhoffs-mansion/
drwxr-xr-x. 2 root   root     57 Dec 23 19:57 /home/tklein/display_chown/
drwxrwxr-x. 2 tklein tklein    6 Dec 23 13:27 /home/tklein/donald_duck/
drwxrwxr-x. 2 tklein tklein   22 Dec 24 06:06 /home/tklein/film/
drwxrwxr-x. 2 tklein tklein    6 Dec 23 13:27 /home/tklein/morganas_secrets/
drwxrwxr-x. 3 tklein tklein   28 Dec 23 14:03 /home/tklein/seinfeld/
drwxrwxr-x. 3 tklein tklein   26 Dec 23 14:52 /home/tklein/the_great_adventure/
~ $
```

In both cases, the number of directories found can be printed instead of the output from `ls -ld */` by adding a pipe and running `wc -l` on the piped output from the `ls -ld */` command.

```bash
~ $ ls -ld /home/tklein/*/ | wc -l
8
~ $
```

#### Printing the number of grep matches in a file

This file is used in the following example\:

```bash
~ $ cat cars/overview
compact-category
convertible-category
coupe-category
cross-over-category
muscle-category
offroad-category
sedan-category
shooting_break-category
sports-category
station_wagon-category
super-category
suv-category
van-category
vintage-category
electrical-category
coupe-category
~ $
```

Every line has '-category' and therefore 16 lines match the search pattern.

```bash
~ $ grep category cars/overview | wc -l
16
~ $
```

### Compare Files (diff and cmp)

There are two main commands used to compare files (**diff files**)

-   `diff` (line by line)
-   `cmp` (byte by byte)

#### diff files

```bash
~ $ diff cars/overview cars/overview2
16a17,19
> bicycle-category
> helicopter-category
> airplane-category
~ $
```

### Compress and Uncompress (tar, gzip, gunzip)

Main commands used\:

-   `tar`
    -   Idea\: Puts several files together into a container, compression is not highest.
-   `gzip`
-   `gzip -d` or `gunzip`
    -   Unarchive\\/Uncompress  the files again

#### tar

##### tar cvf

-   Description of the effect of the options used\:
    -   Contents will be compressed slightly.
    -   Everything will be put into a file.

```bash
~ $ tar cvf tklein.tar .
./
./.bash_logout
./.bash_profile
./.cache/
./.cache/abrt/
./.cache/abrt/lastnotification
./.config/
./.config/abrt/
./.bash_history
./check
./david-hasselhoff
./pamela-anderson
./special_reward
./seinfeld/
./seinfeld/seinfeld_sings/
./seinfeld/seinfeld_sings/to_piano/
./donald_duck/
./morganas_secrets/
./david-hasselhoffs-mansion/
./cars/
./cars/sports-category
./cars/muscle-category
./cars/convertible-category
./cars/compact-category
./cars/super-category
./cars/vintage-category
./cars/sedan-category
./cars/station_wagon-category
./cars/offroad-category
./cars/coupe-category
./cars/shooting_break-category
./cars/van-category
./cars/cross-over-category
./cars/overview_backup
./cars/cars.csv
./cars/cars_backup.csv
./cars/suv-category
./cars/overview
./cars/etc-messages-output
./cars/overview2
./david
./the_great_adventure/
./the_great_adventure/introduction/
./display_chown/
./display_chown/bruce_lee_knows
./display_chown/bruce_lee_chronicles
tar: ./messages: Cannot open: Permission denied
./messages_head50
./messages_tail30
./.bashrc.bak
./]
./.lesshst
./Film.csv
./film/
./film/Film.csv
./.bashrc
./.viminfo
tar: ./tklein.tar: file is the archive; not dumped
tar: Exiting with failure status due to previous errors
~ $ ls -ltr
total 280
-rw-rw-r--. 1 tklein tklein      0 Dec 23 13:26 special_reward
-rw-rw-r--. 1 tklein tklein      0 Dec 23 13:26 pamela-anderson
-rw-rw-r--. 1 tklein tklein      0 Dec 23 13:26 david-hasselhoff
-rw-rw-r--. 1 tklein tklein      0 Dec 23 13:26 check
drwxrwxr-x. 2 tklein tklein      6 Dec 23 13:27 morganas_secrets
drwxrwxr-x. 2 tklein tklein      6 Dec 23 13:27 donald_duck
drwxrwxr-x. 2 tklein tklein      6 Dec 23 13:28 david-hasselhoffs-mansion
-rw-rw-r--. 1 tklein tklein      0 Dec 23 13:47 david
drwxrwxr-x. 3 tklein tklein     28 Dec 23 14:03 seinfeld
drwxrwxr-x. 3 tklein tklein     26 Dec 23 14:52 the_great_adventure
drwxr-xr-x. 2 root   root       57 Dec 23 19:57 display_chown
-rw-------. 1 root   root   183192 Dec 23 21:46 messages
-rw-r--r--. 1 root   root     5565 Dec 23 21:53 messages_head50
-rw-r--r--. 1 root   root     2233 Dec 23 23:00 messages_tail30
-rw-rw-r--. 1 tklein tklein   1144 Dec 24 03:23 ]
-rwxr-xr-x. 1 tklein tklein   5137 Dec 24 06:05 Film.csv
drwxrwxr-x. 2 tklein tklein     22 Dec 24 06:06 film
drwxrwxr-x. 2 tklein tklein   4096 Dec 24 11:29 cars
-rw-rw-r--. 1 tklein tklein  71680 Dec 24 11:46 tklein.tar
~ $
```

### Truncate File Size (truncate)

-   The Linux command `truncate` is often used to shrink or extend the size of a file to a specified size.
-   The command is destructive, if used to shrink a file.
-   Command\: `truncate \[OPTION]... \[FILE]...`
    -   With the `-s n` option, `n` being the desired final file size after running the command.`n` without any following unit specification defaults to bytes

A file named 'cars_are_best' is used in the following. It has a size of 288 bytes.

```bash
~ $ ls -l cars_are_best
-rw-rw-r--. 1 tklein tklein 288 Dec 24 13:18 cars_are_best
~ $
```

Running `truncate -s 100 cars_are_best` truncates the file to the specified 100 bytes and erases text conent inside the file, until it is 100 bytes in size.

```bash
~ $ truncate -s 100 cars_are_best
~ $ ls -l cars_are_best
-rw-rw-r--. 1 tklein tklein 100 Dec 24 13:25 cars_are_best
~ $ cat cars_are_best
The faster the car, the quicker it covers distance.
A V12 engine is a twelve-cylinder piston engine ~ $
```

The command can also be used to extend the size of a file, like in the following example. The command can not restore or add valid data to a file, in order to increase it\\'s size.
Instead, it adds a line of text, of sufficient length to the file until the desired size has been reached.

```bash
The faster the car, the quicker it covers distance.
A V12 engine is a twelve-cylinder piston engine ^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@
~
```

### Combining and Splitting Files

Combining and splitting files can become relevant, if one has to transfer large files. It can become highly relevant in the case of one only having limited storage space, think USB-sticks or CD-Roms \\/ DVDs for example.

-   Cases\:
    		\- Multiple files are combined into one file.
    		\- A single file is split into multiple files.

#### Combining files using cat

5 files are created and populated in one line. All files have the line of text "Combining and Splitting is a lot of fun Yey" as content, see 2. for details.

**1.**

```bash
~ $ echo "Combining and Splitting is a lot of fun Yey" | tee combine_split_file-{0,3,4} > combine_split_file-2
~ $ ls -ltr
total 236
-rw-rw-r--.  1 tklein tklein      0 Dec 23 13:26 special_reward
-rw-rw-r--.  1 tklein tklein      0 Dec 23 13:26 pamela-anderson
-rw-rw-r--.  1 tklein tklein      0 Dec 23 13:26 david-hasselhoff
-rw-rw-r--.  1 tklein tklein      0 Dec 23 13:26 check
drwxrwxr-x.  2 tklein tklein      6 Dec 23 13:27 morganas_secrets
drwxrwxr-x.  2 tklein tklein      6 Dec 23 13:27 donald_duck
drwxrwxr-x.  2 tklein tklein      6 Dec 23 13:28 david-hasselhoffs-mansion
-rw-rw-r--.  1 tklein tklein      0 Dec 23 13:47 david
drwxrwxr-x.  3 tklein tklein     28 Dec 23 14:03 seinfeld
drwxrwxr-x.  3 tklein tklein     26 Dec 23 14:52 the_great_adventure
drwxr-xr-x.  2 root   root       57 Dec 23 19:57 display_chown
-rw-------.  1 root   root   183192 Dec 23 21:46 messages
-rw-r--r--.  1 root   root     5565 Dec 23 21:53 messages_head50
-rw-r--r--.  1 root   root     2233 Dec 23 23:00 messages_tail30
-rw-rw-r--.  1 tklein tklein   1144 Dec 24 03:23 ]
-rwxr-xr-x.  1 tklein tklein   5137 Dec 24 06:05 Film.csv
drwxrwxr-x.  2 tklein tklein     22 Dec 24 06:06 film
drwxrwxr-x.  2 tklein tklein   4096 Dec 24 11:29 cars
drwx------. 12 tklein tklein   4096 Dec 24 11:52 fun_with_files
-rw-rw-r--.  1 tklein tklein    288 Dec 24 13:50 cars_are_best
-rw-rw-r--.  1 tklein tklein     44 Dec 24 14:12 combine_split_file-1
-rw-rw-r--.  1 tklein tklein     44 Dec 24 14:15 combine_split_file-4
-rw-rw-r--.  1 tklein tklein     44 Dec 24 14:15 combine_split_file-3
-rw-rw-r--.  1 tklein tklein     44 Dec 24 14:15 combine_split_file-2
-rw-rw-r--.  1 tklein tklein     44 Dec 24 14:15 combine_split_file-0
~ $
```

**2.**

```bash
~ $ cat combine_split_file-*
Combining and Splitting is a lot of fun Yey
Combining and Splitting is a lot of fun Yey
Combining and Splitting is a lot of fun Yey
Combining and Splitting is a lot of fun Yey
Combining and Splitting is a lot of fun Yey
~ $
```

The 5 files can be combined into another file. The contents of each file are concatenated in the destination file, by appending each file's line(s) of content in the order the input files have been given to the command by the user.

```bash
~ $ cat combine_split_file-* > the_reunion
~ $ cat the_reunion
Combining and Splitting is a lot of fun Yey
Combining and Splitting is a lot of fun Yey
Combining and Splitting is a lot of fun Yey
Combining and Splitting is a lot of fun Yey
Combining and Splitting is a lot of fun Yey
~ $
```

#### Split files using split

```bash
~ $ split -l 2 the_reunion reunited
~ $ ls -ltr
...
-rw-rw-r--.  1 tklein tklein     44 Dec 24 14:35 reunitedac
-rw-rw-r--.  1 tklein tklein     88 Dec 24 14:35 reunitedab
-rw-rw-r--.  1 tklein tklein     88 Dec 24 14:35 reunitedaa
~ $
```

After having split the file 'the_reunion' into files that all have 2 lines each, one can see that 'the reunion' was split into 3 files, that were automatically created, after the declaration of the parent file was done.

```bash
~ $ cat reunitedaa
Combining and Splitting is a lot of fun Yey
Combining and Splitting is a lot of fun Yey
~ $ cat reunitedab
Combining and Splitting is a lot of fun Yey
Combining and Splitting is a lot of fun Yey
~ $ cat reunitedac
Combining and Splitting is a lot of fun Yey
~ $
```

### Linux vs. Windows Commands

|             Command Description             |   Windows  |    Linux    |
| :-----------------------------------------: | :--------: | :---------: |
|            Listing of a directory           |     dir    |    ls -l    |
|               Renaming a file               |     ren    |      mv     |
|                Copying a file               |    copy    |      cp     |
|                Moving a file                |    move    |      mv     |
|       Clearing the command line window      |     cls    |    clear    |
|               Deleting a file               |     del    |      rm     |
|         Comparing contents of files         |     fc     |     diff    |
|    Searching for a word/string in a file    |    find    |     grep    |
|          Displaying a command help          | command /? | man command |
| Displaying your location in the file system |    chdir   |     pwd     |
|             Displaying the time             |    time    |     date    |

## Module 5 - System Administration

### 'video'

## Module 6 - Shell Scripting

### 'video'

## Module 7 - Networking, Services and System Updates

### 'video'

## Module 8 - Disk Management and Run Levels

### 'video'
