---
title: 'Recap: Exercises - Module 4'
subtitle: 'Learning Linux - Section 4 Exercises'
date: 2021-12-29 00:00:00
description: 'This post covers solving exercises, to help foster longterm retention of the content in Module4'
featured_image: bash-ga254901e3_1280.png
gallery_images: Bash_GNOME_Terminal_screenshot.png
accent_color: '#4C60E6'
---

### Module 4 - Exercises

Practice Linux command syntax with\:
- command
- options
- arguments

#### Listing files

> List files in your home directory by the last time they were modified.

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

> Move files jerry, george, kramer, puddy to the seinfeld directory.

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

---

> Move homer, bart, marge, lisa to the simpsons directory.

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
---

  > Move clark, luther and lois files to the superman directory

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

---

> List the contents of the seinfeld directory by the last time they were modified

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

---

> Create 2 new files in the seinfeld directory, eliane and newman.


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

---

> Change the file permissions for 'eliane', so that read access is revoked for 'everyone'.

- There is no file named 'eliane' in the current directory and so it is created using `touch eliane` as an empty text file.
- Next, the current permissions are checked for the file. This change can be omitted when not using the `chmod` together with the octal representation for `user`, `group` and `everyone`.
- The permissions for `user` and `group` are not to be changed, so they stay the same ('66').
-   `everyone` currently has permissions equal to '1' in the octal representation. That translates to 'read only' permissions for `everyone` for the file 'eliane'.
- 'read' permissions are revoked for `everyone`, by changing permissions to '0'.
- Running `ls -l eliane` confirms the changes.

```bash
~ $ ls -ltr | grep "eli"
~ $ touch eliane
~ $ ls -l eliane
-rw-rw-r--. 1 tklein tklein 0 Dec 25 04:07 eliane
~ $ chmod 660 eliane
~ $ ls -l eliane
-rw-rw----. 1 tklein tklein 0 Dec 25 04:07 eliane
~ $
```

Now, there was an error and the file actually already exists in the directory `seinfeld/`. For the file inside the `seinfeld/` directory to have it\'s permissions changed without the risk of overwriting it\'s contents and deleting them by copying the empty file 'eliane' to `seinfeld/eliane` for example, one can use `chmod --reference=RFILE FILE`, like that only the permissions get applied to `seinfeld/eliane` from `./eliane`.

```bash
~ $ chmod --reference=eliane seinfeld/eliane
~ $ ls -l seinfeld/eliane
-rw-rw----. 1 tklein tklein 0 Dec 25 00:41 seinfeld/eliane
~ $
```
