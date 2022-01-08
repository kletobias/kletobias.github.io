---
title: 'Recap: Exercises - Module 4'
subtitle: 'Learning Linux - Section 4 Exercises'
date: 2021-11-25 00:00:00
description: 'This post covers solving exercises, to help foster longterm retention of the content in Module4'
featured_image: 'mT68055%25%25--tYF_5__5jhhh5pls$0-G.jpeg'
gallery_images: 'YtOk89__87-kbtTGW$DD-L.jpeg'
accent_color: '#08877d'
---

### Module 4 - Exercises

Practice Linux command syntax with\:
- command
- options
- arguments

#### Listing files

##### *List files in your home directory by the last time they were modified.*

Using `ls` to print the contents of my home directory with options `-ltcr` gives the desired output. The options do\:
- `l` Print contents using the long format, so 'last time modified' is printed.
- `tc` sort by 'last modified'
- `r` reverse sorting order to print 'last time modified' in acending order \(from old to more recent). Most recently modified file will be printed at the bottom of the output.

```bash
~ $ whoami
tklein
~ $ hostname
localhost.localdomain
~ $ pwd
/home/tklein
~ $ ls -ltcr
total 256
-rw-rw-r--.  1 tklein tklein      0 Dec 23 13:26 pamela-anderson
-rw-rw-r--.  1 tklein tklein      0 Dec 23 13:26 david-hasselhoff
-rw-rw-r--.  1 tklein tklein      0 Dec 23 13:26 check
drwxrwxr-x.  2 tklein tklein      6 Dec 23 13:27 morganas_secrets
drwxrwxr-x.  2 tklein tklein      6 Dec 23 13:27 donald_duck
drwxrwxr-x.  2 tklein tklein      6 Dec 23 13:28 david-hasselhoffs-mansion
-rw-rw-r--.  1 tklein tklein      0 Dec 23 13:47 david
drwxrwxr-x.  3 tklein tklein     28 Dec 23 14:03 seinfeld
drwxrwxr-x.  3 tklein tklein     26 Dec 23 14:52 the_great_adventure
-rw-rw-r--.  1 tklein tklein      0 Dec 23 19:35 special_reward
drwxr-xr-x.  2 root   root       57 Dec 23 19:57 display_chown
-rw-------.  1 root   root   183192 Dec 23 21:46 messages
-rw-r--r--.  1 root   root     5565 Dec 23 21:53 messages_head50
-rw-r--r--.  1 root   root     2233 Dec 23 23:00 messages_tail30
-rwxr-xr-x.  1 tklein tklein   5137 Dec 24 06:05 Film.csv
drwxrwxr-x.  2 tklein tklein     22 Dec 24 06:06 film
drwxrwxr-x.  2 tklein tklein   4096 Dec 24 11:29 cars
drwx------. 12 tklein tklein   4096 Dec 24 11:52 fun_with_files
-rw-rw-r--.  1 tklein tklein     44 Dec 24 14:12 combine_split_file-1
-rw-rw-r--.  1 tklein tklein     44 Dec 24 14:15 combine_split_file-4
-rw-rw-r--.  1 tklein tklein     44 Dec 24 14:15 combine_split_file-3
-rw-rw-r--.  1 tklein tklein     44 Dec 24 14:15 combine_split_file-2
-rw-rw-r--.  1 tklein tklein     44 Dec 24 14:15 combine_split_file-0
-rw-rw-r--.  1 tklein tklein    220 Dec 24 14:23 the_reunion
-rw-rw-r--.  1 tklein tklein     44 Dec 24 14:35 reunitedac
-rw-rw-r--.  1 tklein tklein     88 Dec 24 14:35 reunitedab
-rw-rw-r--.  1 tklein tklein     88 Dec 24 14:35 reunitedaa
-rw-rw-r--.  1 tklein tklein    184 Dec 24 20:34 cars_are_best
-rw-rw-r--.  1 tklein tklein    120 Dec 24 22:40 learning_vim1
-rw-rw-r--.  1 tklein tklein   1437 Dec 24 23:31 ddr4_vs_5
-rw-rw-r--.  1 tklein tklein      0 Dec 25 00:13 kramer
-rw-rw-r--.  1 tklein tklein      0 Dec 25 00:13 jerry
-rw-rw-r--.  1 tklein tklein      0 Dec 25 00:13 george
-rw-rw-r--.  1 tklein tklein      0 Dec 25 00:13 puddy
-rw-rw-r--.  1 tklein tklein      0 Dec 25 00:13 marge
-rw-rw-r--.  1 tklein tklein      0 Dec 25 00:13 luther
-rw-rw-r--.  1 tklein tklein      0 Dec 25 00:13 lois
-rw-rw-r--.  1 tklein tklein      0 Dec 25 00:13 lisa
-rw-rw-r--.  1 tklein tklein      0 Dec 25 00:13 homer
-rw-rw-r--.  1 tklein tklein      0 Dec 25 00:13 clark
-rw-rw-r--.  1 tklein tklein      0 Dec 25 00:13 bart
```

#### Moving files into directories

##### *Move files jerry, george, kramer, puddy to the seinfeld directory.*

Using `mv`, all the input files are listed first separated by ' ' and the destination directory is put last.

```bash
~ $ mv jerry george kramer puddy seinfeld/
~ $ ls -lrc seinfeld
total 0
drwxrwxr-x. 3 tklein tklein 22 Dec 23 14:03 seinfeld_sings
-rw-rw-r--. 1 tklein tklein  0 Dec 25 00:24 puddy
-rw-rw-r--. 1 tklein tklein  0 Dec 25 00:24 kramer
-rw-rw-r--. 1 tklein tklein  0 Dec 25 00:24 jerry
-rw-rw-r--. 1 tklein tklein  0 Dec 25 00:24 george
~ $
```

##### *Move homer, bart, marge, lisa to the simpsons directory.*

- There is no 'simpsons' folder in the home directory and so the folder is being created first using `mkdir simpsons`
- The same command and structure is used as in the example above to move the files into the destination folder.


```bash
~ $ ls -ltc | grep "simp"
~ $ mkdir simpsons
~ $ mv homer bart marge lisa simpsons/
~ $ ls -ltcr simpsons/
total 0
-rw-rw-r--. 1 tklein tklein 0 Dec 25 00:30 marge
-rw-rw-r--. 1 tklein tklein 0 Dec 25 00:30 lisa
-rw-rw-r--. 1 tklein tklein 0 Dec 25 00:30 homer
-rw-rw-r--. 1 tklein tklein 0 Dec 25 00:30 bart
~ $
```

##### *Move clark, luther and lois files to the superman directory.*

Again, the directory 'superman' and 'Superman' are not existent yet and so are created and finally the files are being moved into the new directory 'superman'.

```bash
~ $ ls -ltcr | grep "superman"
~ $ ls -ltcr | grep "Superman"
~ $ mkdir superman
~ $ mv clark luther lois superman/
~ $ ls -ltcr superman/
total 0
-rw-rw-r--. 1 tklein tklein 0 Dec 25 00:33 luther
-rw-rw-r--. 1 tklein tklein 0 Dec 25 00:33 lois
-rw-rw-r--. 1 tklein tklein 0 Dec 25 00:33 clark
~ $
```

##### *List the contents of the seinfeld directory by the last time they were modified*

```bash
~ $ ls -ltcr seinfeld
total 0
drwxrwxr-x. 3 tklein tklein 22 Dec 23 14:03 seinfeld_sings
-rw-rw-r--. 1 tklein tklein  0 Dec 25 00:24 puddy
-rw-rw-r--. 1 tklein tklein  0 Dec 25 00:24 kramer
-rw-rw-r--. 1 tklein tklein  0 Dec 25 00:24 jerry
-rw-rw-r--. 1 tklein tklein  0 Dec 25 00:24 george
~ $
```

##### *Create 2 new files in the seinfeld directory, eliane and newman.*


```bash
~ $ touch seinfeld/eliane seinfeld/newman
~ $ ls -ltcr seinfeld
total 0
drwxrwxr-x. 3 tklein tklein 22 Dec 23 14:03 seinfeld_sings
-rw-rw-r--. 1 tklein tklein  0 Dec 25 00:24 puddy
-rw-rw-r--. 1 tklein tklein  0 Dec 25 00:24 kramer
-rw-rw-r--. 1 tklein tklein  0 Dec 25 00:24 jerry
-rw-rw-r--. 1 tklein tklein  0 Dec 25 00:24 george
-rw-rw-r--. 1 tklein tklein  0 Dec 25 00:41 newman
-rw-rw-r--. 1 tklein tklein  0 Dec 25 00:41 eliane
~ $
```

##### *Change the file permissions for 'eliane', so that read access is revoked for 'everyone'.*

- There is no file named 'eliane' in the current directory and so it is created using `touch eliane` as an empty text file.
- Next, the current permissions are checked for the file. This change can be omitted when not using the `chmod` together with the octal representation for `user`, `group` and `other`.
- The permissions for `user` and `group` are '6' for each one at the start.
-   `other` currently has permissions equal to '4' in the octal representation. That translates to 'read only' permissions for `other` for the file 'eliane'.
- 'read' permissions are revoked for everyone, by subtracting '4' from each group\'s current permissions. That means, the new permissions will be for 'user','group' and 'other'\: `220`
- Running `ls -l eliane` confirms the changes.

```bash
~ $ ls -ltr | grep "eli"
~ $ touch eliane
~ $ ls -l eliane
-rw-rw-r--. 1 tklein tklein 0 Dec 25 04:07 eliane
~ $ chmod 220 eliane
~ $ ls -l eliane
--w--w----. 1 tklein tklein 0 Dec 25 04:07 eliane
~ $
```

Now, there was an error and the file actually already exists in the directory `seinfeld/`. For the file inside the `seinfeld/` directory to have it\'s permissions changed without the risk of overwriting it\'s contents and deleting them by copying the empty file 'eliane' to `seinfeld/eliane` for example, one can use `chmod --reference=RFILE FILE`, like that only the permissions get applied to `seinfeld/eliane` from `./eliane`.

```bash
~ $ ls -l seinfeld/eliane
-rw-rw-r--. 1 tklein tklein 0 Dec 25 00:41 seinfeld/eliane
~ $ chmod --reference=eliane seinfeld/eliane
~ $ ls -l seinfeld/eliane
--w--w----. 1 tklein tklein 0 Dec 25 00:41 seinfeld/eliane
~ $
```

Another option is the following one. Here it is used to restore the permissions of the file.


```bash
~ $ chmod u+r,g+r,o+r eliane
~ $ ls -l eliane
-rw-rw-r--. 1 tklein tklein 0 Dec 25 00:41 eliane
~ $
```

##### *Change the permissions of file newman to remove write permissions only from group.*

Using the methods from the exercise prior to this one\:

```bash
~ $ ls -l newman
-rw-rw-r--. 1 tklein tklein 0 Dec 25 00:41 newman
~ $ chmod 644 newman
~ $ ls -l newman
-rw-r--r--. 1 tklein tklein 0 Dec 25 00:41 newman
~ $ chmod 664 newman
~ $ ls -l newman
-rw-rw-r--. 1 tklein tklein 0 Dec 25 00:41 newman
~ $ chmod g-w newman
~ $ ls -l newman
-rw-r--r--. 1 tklein tklein 0 Dec 25 00:41 newman
~ $
```

##### *Become root and cd into your home directory. Then create 2 new files superman and zad in superman directory*

```bash
root * touch superman/superman superman/zad
root * ls -l superman/
total 0
-rw-rw-r--. 1 tklein tklein 0 Dec 25 00:13 clark
-rw-rw-r--. 1 tklein tklein 0 Dec 25 00:13 lois
-rw-rw-r--. 1 tklein tklein 0 Dec 25 00:13 luther
-rw-r--r--. 1 root   root   0 Dec 25 07:46 superman
-rw-r--r--. 1 root   root   0 Dec 25 07:46 zad
root *
```

##### *Change ownership of zad file from root to your username*


```bash
root * chown tklein superman/zad
root * ls -l superman/zad
-rw-r--r--. 1 tklein root 0 Dec 25 07:46 superman/zad
root *
```

##### *Change group ownership of zad from root to your username*

```bash
root * chown tklein:root superman/zad
root * ls -l superman/zad
-rw-r--r--. 1 tklein root 0 Dec 25 07:46 superman/zad
root * chown tklein:root superman/zad
root * chown :tklein superman/zad
root * ls -l superman/zad
-rw-r--r--. 1 tklein tklein 0 Dec 25 07:46 superman/zad
root *
```

##### *Then move the superman file to /tmp directory*
##### *Remove superman file from /tmp directory*
##### *Exit out of root account*

```bash
root * mv superman/superman /tmp/
root * rm -f /tmp/superman
root * ls -l /tmp | grep "super"
root * exit
exit
~ $
```

##### *Go back to superman directory in your home directory and add this line to the 'zad' file\: \"zad is a bad character in the superman movie.\"*

```bash
~ $ cd superman/
~ $ echo "zad is a bad character in the superman movie." >> zad
~ $ cat zad
zad is a bad character in the superman movie.
~ $
```

##### *Go to the seinfeld directory and create a new file named \'seinfeld\'.*

```bash
~ $ pwd
/home/tklein/superman
~ $ cd
~ $ cd seinfeld/
~ $ ls -l
total 0
-rw-rw-r--. 1 tklein tklein  0 Dec 25 00:41 eliane
-rw-rw-r--. 1 tklein tklein  0 Dec 25 00:13 george
-rw-rw-r--. 1 tklein tklein  0 Dec 25 00:13 jerry
-rw-rw-r--. 1 tklein tklein  0 Dec 25 00:13 kramer
-rw-r--r--. 1 tklein tklein  0 Dec 25 00:41 newman
-rw-rw-r--. 1 tklein tklein  0 Dec 25 00:13 puddy
drwxrwxr-x. 3 tklein tklein 22 Dec 23 14:03 seinfeld_sings
~ $ touch seinfeld
~ $
```

##### *Add 5 seinfeld characters\' names in seinfeld file. Jerry Seinfeld, George Costanza, Eliane Benis, Cosmo Kramer, and David Puddy*

```bash
~ $ pwd
/home/tklein/seinfeld
~ $ touch 'Jerry Seinfeld' 'George Costanza' 'Eliane Benis' 'David Puddy'
~ $ ls -ltr
total 0
drwxrwxr-x. 3 tklein tklein 22 Dec 23 14:03 seinfeld_sings
-rw-rw-r--. 1 tklein tklein  0 Dec 25 00:13 kramer
-rw-rw-r--. 1 tklein tklein  0 Dec 25 00:13 jerry
-rw-rw-r--. 1 tklein tklein  0 Dec 25 00:13 george
-rw-rw-r--. 1 tklein tklein  0 Dec 25 00:13 puddy
-rw-r--r--. 1 tklein tklein  0 Dec 25 00:41 newman
-rw-rw-r--. 1 tklein tklein  0 Dec 25 00:41 eliane
-rw-rw-r--. 1 tklein tklein  0 Dec 25 08:04 seinfeld
-rw-rw-r--. 1 tklein tklein  0 Dec 25 08:07 Jerry Seinfeld
-rw-rw-r--. 1 tklein tklein  0 Dec 25 08:07 George Costanza
-rw-rw-r--. 1 tklein tklein  0 Dec 25 08:07 Eliane Benis
-rw-rw-r--. 1 tklein tklein  0 Dec 25 08:07 David Puddy
~ $
```

##### *Do cat /var/log/messages and output to a file called mesg-new in your home directory.*

Becoming root again for the following.

```bash
~ $ su
Password:
root *
```

```bash
root * cat /var/log/messages > /home/tklein/mesg-new
root * head -6 /home/tklein/mesg-new
Dec 23 13:16:58 localhost journal: Runtime journal is using 6.1M (max allowed 48.9M, trying to leave 73.3M free of 483.1M available → current limit 48.9M).
Dec 23 13:16:58 localhost kernel: Initializing cgroup subsys cpuset
Dec 23 13:16:58 localhost kernel: Initializing cgroup subsys cpu
Dec 23 13:16:58 localhost kernel: Initializing cgroup subsys cpuacct
Dec 23 13:16:58 localhost kernel: Linux version 3.10.0-1160.el7.x86_64 (mockbuild@kbuilder.bsys.centos.org) (gcc version 4.8.5 20150623 (Red Hat 4.8.5-44) (GCC) ) #1 SMP Mon Oct 19 16:18:59 UTC 2020
Dec 23 13:16:58 localhost kernel: Command line: BOOT_IMAGE=/vmlinuz-3.10.0-1160.el7.x86_64 root=/dev/mapper/centos-root ro crashkernel=auto spectre_v2=retpoline rd.lvm.lv=centos/root rd.lvm.lv=centos/swap rhgb quiet LANG=en_US.UTF-8
root *
```

##### *Read the mesg-new file with cat, more and less commands and practice.*

Since cat would print the entire file, which has 3606 lines, the output was not included in here.

```bash
~ $ wc -l mesg-new
3606 mesg-new
~ $
```

`more` and `less` also print large chunks of text overall in this example and so only a description of both commands is done in the following.

##### 'more'

`~ $ more mesg-new` will print the lines from file `mesg-new` one screen at a time and by pressing the 'space bar' once, it will advance one screen further down. `more` can only move downwards and never upwards in the file.

##### 'less'

`~ $ less mesg-new` will have all the functionality of `more` with the addition of more commands for the user to navigate the output it generates.

The printing of the output can be stopped for both commands, by hitting the 'q' key on the keyboard.

##### *View the first 10 lines of mesg-new file and output to a file name mesg-h10*

Only 2 lines are printed to keep the ouput from taking to much space to be printed in this article. The lines are counted to verify that the newly created file has indeed 10 lines.

```bash
~ $ head -2 mesg-h10 && wc -l mesg-h10
Dec 23 13:16:58 localhost journal: Runtime journal is using 6.1M (max allowed 48.9M, trying to leave 73.3M free of 483.1M available → current limit 48.9M).
Dec 23 13:16:58 localhost kernel: Initializing cgroup subsys cpuset
10 mesg-h10
```

##### *View the last 20 lines of mesg-new file and output to a file name mesg-t20*

Running all commands after one another, using the notation `&&` to seperate them from one another. They are being executed in the order they are specified. It goes from left to right. Like this, in the example below, the user can use a not yet created file named 'mesg-t20' for the second and third chained command, that is created after execution of the most left command in the chain.

```bash
~ $ tail -20 mesg-new > mesg-t20 && head -2 mesg-t20 && wc -l mesg-t20
Dec 25 07:50:01 localhost systemd: Started Session 313 of user root.
Dec 25 07:50:01 localhost systemd: Removed slice User Slice of root.
20 mesg-t20
~ $
```

##### *Go to seinfeld directory in your home directory and create a new file "seinfeld-characters"*

```bash
~ $ touch seinfeld-characters
~ $ ls -l seinfeld-characters
-rw-rw-r--. 1 tklein tklein 0 Dec 25 11:14 seinfeld-characters
~ $
```

##### *Add text to seinfeld-character file using echo command. Each character  should be in one line, "Jerry Seinfeld, Cosmo Kramer, Eliane Benes,  George Costanza, Newman Mailman, Frank Costanza, Estelle Costanza,  Morty Seinfeld, Helen Seinfeld, Babes Kramer, Alton Benes, J Peterman,  George Steinbrenner, Uncle Leo, David Puddy, Justin Pit and Kenny Bania"*

Using option `-e` from the `echo` command, new lines can be entered using `\n`. One has to make sure, that what comes on the next line is written immediately after `\n` with no space in between.

```bash
~ $ echo -e "Jerry Seinfeld,\nCosmo Kramer,\nEliane Benes,\nGeorge Costanza,\nNewman Mailman,\nFrank Costanza,\nEstelle Costanza,\nMorty Seinfeld,\nHelen Seinfeld,\nBabes Kramer,\nAlton Benes,\nJ Peterman,\nGeorge Steinbrenner,\nUncle Leo,\nDavid Puddy,\nJustin Pit,\nKenny Bania" > seinfeld-characters
~ $ cat seinfeld-characters
Jerry Seinfeld,
Cosmo Kramer,
Eliane Benes,
George Costanza,
Newman Mailman,
Frank Costanza,
Estelle Costanza,
Morty Seinfeld,
Helen Seinfeld,
Babes Kramer,
Alton Benes,
J Peterman,
George Steinbrenner,
Uncle Leo,
David Puddy,
Justin Pit,
Kenny Bania
~ $
```

##### *Use cut command to cut the first 4 letters of each line from seinfeld-characters file and output to a different file.*

`cut` is used with option `-c`, so that it only cuts the selected characters on each line. Here, the range is from character `1` to `4`. This can be achieved by writing the following command\:

`cut -c1-4 seinfeld-characters`

 Again, a second command is chained after the first one is executed to print the lines of the new file, that the output was redirected to.

```bash
~ $ cut -c1-4 seinfeld-characters  > seinfeld-characters_first4 && cat seinfeld-characters_first4
Jerr
Cosm
Elia
Geor
Newm
Fran
Este
Mort
Hele
Babe
Alto
J Pe
Geor
Uncl
Davi
Just
Kenn
~ $
```

##### *Use awk command to get only the 2nd column of seinfeld-characters and output to the seinfeld-characters_first4 without removing any other text from it*

```bash
~ $ awk '{print $2}' seinfeld-characters >> seinfeld-characters_first4
~ $ cat seinfeld-characters_first4
Jerr
Cosm
Elia
Geor
Newm
Fran
Este
Mort
Hele
Babe
Alto
J Pe
Geor
Uncl
Davi
Just
Kenn
Seinfeld,
Kramer,
Benes,
Costanza,
Mailman,
Costanza,
Costanza,
Seinfeld,
Seinfeld,
Kramer,
Benes,
Peterman,
Steinbrenner,
Leo,
Puddy,
Pit,
Bania
~ $
```

##### *Use grep command to only grep seinfeld and output to a new file call it only_seinfelds*

Using grep with option `-i`, one can match the specified pattern non case-sensitive.

```bash
~ $ grep -i "seinfeld" seinfeld-characters > only_seinfelds
~ $ cat only_seinfelds
Jerry Seinfeld,
Morty Seinfeld,
Helen Seinfeld,
~ $
```

##### *Use sort command, uniq and wc command to practice whichever way you like by creating new files or working with existing files*

```bash
~ $ sort seinfeld-characters
Alton Benes,
Babes Kramer,
Cosmo Kramer,
David Puddy,
Eliane Benes,
Estelle Costanza,
Frank Costanza,
George Costanza,
George Steinbrenner,
Helen Seinfeld,
J Peterman,
Jerry Seinfeld,
Justin Pit,
Kenny Bania
Morty Seinfeld,
Newman Mailman,
Uncle Leo,
```

```bash
~ $ sort -r seinfeld-characters
Uncle Leo,
Newman Mailman,
Morty Seinfeld,
Kenny Bania
Justin Pit,
Jerry Seinfeld,
J Peterman,
Helen Seinfeld,
George Steinbrenner,
George Costanza,
Frank Costanza,
Estelle Costanza,
Eliane Benes,
David Puddy,
Cosmo Kramer,
Babes Kramer,
Alton Benes,
```

```bash
~ $ sort -k2 seinfeld-characters
Kenny Bania
Alton Benes,
Eliane Benes,
Estelle Costanza,
Frank Costanza,
George Costanza,
Babes Kramer,
Cosmo Kramer,
Uncle Leo,
Newman Mailman,
J Peterman,
Justin Pit,
David Puddy,
Helen Seinfeld,
Jerry Seinfeld,
Morty Seinfeld,
George Steinbrenner,
```

```bash
~ $ sort -r -k2 seinfeld-characters
George Steinbrenner,
Morty Seinfeld,
Jerry Seinfeld,
Helen Seinfeld,
David Puddy,
Justin Pit,
J Peterman,
Newman Mailman,
Uncle Leo,
Cosmo Kramer,
Babes Kramer,
George Costanza,
Frank Costanza,
Estelle Costanza,
Eliane Benes,
Alton Benes,
Kenny Bania
~ $
```

##### 'uniq'

```bash
~ $ uniq seinfeld-characters
Jerry Seinfeld,
Cosmo Kramer,
Eliane Benes,
George Costanza,
Newman Mailman,
Frank Costanza,
Estelle Costanza,
Morty Seinfeld,
Helen Seinfeld,
Babes Kramer,
Alton Benes,
J Peterman,
George Steinbrenner,
Uncle Leo,
David Puddy,
Justin Pit,
Kenny Bania
Uncle Leo,
```

```bash
~ $ cat seinfeld-characters
Jerry Seinfeld,
Cosmo Kramer,
Eliane Benes,
George Costanza,
Newman Mailman,
Frank Costanza,
Estelle Costanza,
Morty Seinfeld,
Helen Seinfeld,
Babes Kramer,
Alton Benes,
J Peterman,
George Steinbrenner,
Uncle Leo,
David Puddy,
Justin Pit,
Kenny Bania
Uncle Leo,
~ $
```

##### 'wc'

Counting lines.

```bash
~ $ wc -l seinfeld-characters
18 seinfeld-characters
```

Counting bytes.

```bash
~ $ wc -c seinfeld-characters
262 seinfeld-characters
```

Counting characters.

```bash
~ $ wc -m seinfeld-characters
262 seinfeld-characters
~ $
```

That is it for Section 4.