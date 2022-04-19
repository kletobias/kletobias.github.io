
\\---
title: 'Learning Linux - Chapter 5'
description: 'In chapter 5, \TODO'
date: 2022-03-01 06:00:00
featured_image: 'mT68055%25%25--tYF_5__5jhhh5pls$0-G.jpeg'
gallery_images: 'YtOk89__87-kbtTGW$DD-L.jpeg'
accent_color: '#08877d'
---

---
title: 'Learning Linux - Chapter 5: Section 1 & 2'
description: 'In Chapter 5 Section 1 & 2, we take a look at several Linux text editors and compare the vi text editor to the vim text
editor. Plus, we give an introduction to how to use the vi/vim text editors.'
date: 2022-01-01 05:01:02
featured_image: 'mT68055%25%25--tYF_5__5jhhh5pls$0-G.jpeg'
gallery_images: 'YtOk89__87-kbtTGW$DD-L.jpeg'
accent_color: '#08877d'
---


# Linux Text Editors

**Learning Linux - Section 5.1**


A text editor is a program, that enables one to create and manipulate text data in a Linux file. Popular, standard text editors for Linux are listed in this chapter.

### 5.1 - Linux Text Editors

- A text editor is a program, that enables one to create and manipulate text data in a Linux file.
- Popular, standard text editors for Linux include\:

| Text Editor |        Details         |
|:-----------:|:----------------------:|
|     vi      |     Visual Editor      |
|     ed      |  Standard Line Editor  |
|     ex      |  Extended Line Editor  |
|    emacs    |   Full Screen Editor   |
|    pico     |   Beginner\'s Editor   |
|     vim     | Improved Version of vi |
|    nvim     | neovim                 |


#### Introduction to the vi editor

- vi supplies commands for\:
  - Inserting and deleting text
  - Replacing text
  - Moving around a text file
  - Finding and substituting strings
  - Cutting and pasting text

- Most common keys are among others\:
  - `i` \- insertion mode
  - `Esc` \- Get out of insert or visual mode
  - `r` \- replace
  - `d` \- delete \(line)
  - `:q!` \- quit vi without writing recent changes
  - `:wq` \- write file and quit

##### Writing and exiting a file

There are several options for how to accomplish this\:


1. While in insert mode\:
   1. Hit `Esc` \> `:` \> type\: `wq` on the command line.
   2. Hit `Esc` \> Hit (capital) `Z` `Z` and the file will be saved and vi quits.


##### Moving around a text file

Moving the cursor inside a text file in vi\:
- Moving up one line at a time\: `k`
- Moving down one line at a time\: `j`
- Moving to the left, one character at a time\: `h`
- Using `a` while in normal mod advances the cursor one character and switches to `-- INSERT --` mode.
- A variation of pressing `a` is pressing `SHIFT + a`.This will advance the cursor to the end of the current line and change to `-- INSERT --` mode.
- `SHIFT + h` will move the cursor to the beginning of the file, if pressed in normal mode.
- Using `o` lets the user create a new line just below the cursor and automatically changes the mode to `-- INSERT -`. The cursor is placed on the newly created line and one can start writing on the new line.

##### Deleting and restoring deleted text

###### Deletion

- Keys used to delete text inside vi\:
  - 2 x `d` deletes the entire line, where the cursor is.
  - 1 x `x` deletes the closest character on the right of the cursor position. Using `SHIFT + x` removes the closest character on the left of the cursor.

###### Restoration

- Key used to restore deleted lines or characters\:
  - 1 x `u` is used to restore deleted text.
  - It restores one line per key press, if `d` was used to delete it.
  - If `x` was used, it restores one deleted character per key press.

##### Replacing Text

- Using the key `r` while in normal mode allows one to replace the character immediately right of the current cursor position by pressing the key, that is to replace that current character next to the cursor on it\'s right side.

###### Example

There is a typo in the last word and 'h' should be replaced by 's'

```vim
No CAPS, REALLY: This is good htuff
```

The cursor position is marked by '\|'.

```vim
No CAPS, REALLY: This is good |htuff
```

Pressing 'r', followed by 's', replaces 'h' with 's'.

```vim
No CAPS, REALLY: This is good stuff.
```

##### Moving around the file and manipulating text

- Using `o` lets the user create a new line just below the cursor and automatically changes the mode to `-- INSERT --`. The cursor is placed on the newly created line and one can start writing on the new line.

##### Searching inside a text file

While there are several ways to search for text inside a file, here are two ways of how it can be done\:

- Using the `grep` command, like so\:
   - `grep 'text file' cars_are_best`

```bash
~ $ grep 'text file' cars_are_best
Not just any text file.
~ $
```

- Inside vi\:
   - `/` followed by typing right after the `/` like\:
   - `/text file`


# Differences between vi and vim Editor

**Learning Linux - Section 5.2**


A text editor is a program, that enables one to create and manipulate text data in a Linux file. Popular, standard text editors for Linux are listed in this chapter.


### Differences between vi and vim Editor

As far as functionality is concerned, both editors work in the same manner, as far as basic editing and controls go. There are many plugins available for the vim editor, that add useful features to it. Which editor one chooses is a matter of personal choice. Some people recommend learning the vim editor instead of the vi editor. Due to added features and using vim editor is much easier than the vi editor.

- Some older operating systems have vi support, but not vim support.
- vim has many more features compared to vi, which means that if one is familiar with vim, having to use vi in certain situations is not a problem.
- vim has all the features, that vi has with some excellent additions.
- There is also a comprehensive help system built into vim and there are lots of options when it comes to customising vim as well.

|            Vi            |                  Shared                   |         Vim         |
|:------------------------:|:-----------------------------------------:|:-------------------:|
| installed in more places |                   small                   |   auto completion   |
|       shorter name       |                ubiquitous                 |     spell check     |
|         simpler          | intuitive command language \(d, y, etc\.) | comparison of files |
|                          |           have a learning curve           |    merging files    |
|                          |          powerful once mastered           |       unicode       |
|                          |                                           |     \(vimdiff)      |
|                          |                                           | regular expressions |
|                          |                                           | scripting languages |
|                          |                                           |       plugins       |
|                          |                                           |         GUI         |
|                          |                                           |       folding       |
|                          |                                           | syntax highlighting |


#### vim interactive learning Tools

- There are many websites that offer free vim interactive training
  - <https://www.openvim.com/>
  - <http://www.vimgenius.com>
  - <https://www.vim-adventures.com> (games)


title: 'Learning Linux - Chapter 5: Section 3'
description: 'This section covers some of the essential commands and concepts used in any Linux distribution.'
date: 2022-01-01 05:03:00
featured_image: 'mT68055%25%25--tYF_5__5jhhh5pls$0-G.jpeg'
gallery_images: 'YtOk89__87-kbtTGW$DD-L.jpeg'
accent_color: '#08877d'
---

# `sed` Command

**Learning Linux - Section 5.3**


This article covers some of the essential commands and concepts used in any Linux distribution.

### Introduction

The Vim text editor was used and CentOS 7.4 was the distribution installed on the virtual machine in this series. It was setup as a command line only virtual machine and accessed through ssh. There are 8 Sections in total.

<!---Gallery is used, when listing the articles, featured is the image placed at the top of the article.
-->

`sed` Command

- `sed` replaces a string in a file with a new string.
- It can be used to find and delete a line of a file. Use cases are:
  - Remove empty lines.
  - Remove the first line or `n` lines.
  - Replace tabs with spaces.
  - Show defined lines from a file.
  - Substitute \(replace) within vi editor.
  - And much more...

#### sed \'s/DDR/DNS/g' FILE

- Like this, the command does:
  - `s` substitute
  - `DDR` with `DNS`
	- `g` - do this for all matches in the `FILE` /(`g` == global).
	- It will not write the above changes to the file by default and will only show them on screen.
	- Changes are written, if `-i` is added.


##### Example

The this text file is used in the following examples.

```text
~ $ cat ddr4_vs_5
DDR5 is improvement to existing DDR4 and is similar to LPDDR4.
While DDR4 DIMMs (memory stick) are 64 bits (72 bits with
ECC, so called buffered or registered) DDR5 moved to
2 x 32 bits or 2 x 40 bits for ECC. Btw LPDDR4 is 2 x 16
bits. DDR5 DIMM has two separate 32 bit channels, like two
DDR4 DIMMs - single DDR5 DIMM is dual channel. Additional
improvement is number of burst transfers. While DDR4
is 4 or 8, LPDDR4 16 or 32, DDR5 increased to 16. By
doubling bursts DDR5 despite 32 bits achieves DDR4 speeds.
Btw in x86 CPU (and others too) cache line is 64 bytes what
corresponds to DDR4 64 bits and 8 transfers. Operating
voltage is reduced from 1.2V to 1.1V what reduces power
consumption, eg LPDDR4 is 1V. Additional features are
added which speed up DDR5 further, eg number of banks,
hidden refresh, etc. Also memory sizes are increased.
DDR4 per DIMM is 32GB while DDR5 increases this to 64GB
and further. Additionally transfer speeds are increased.
Latest DDR4 is 3200/3600 (originally 2133 or 2166)
while DDR5 starts at 4800, followed by 5200, 6000 and even
10000. Of course, latencies, famous CL, is also higher
cause internally tech cannot improve too much. Eg DDR4 3200
has CL 16 what is 10 ns while DDR5 4800 is 34 what is 14 ns.
There are more expensive CL 30 DIMMs. So, no big
differences but compensated with longer bursts and higher
transfer speeds. At the end DDR5 is bit faster but
is also way more expensive.
~ $
```

Reading the first line before running `sed` on the file:

```bash
~ $ head -1 ddr4_vs_5
DDR5 is improvement to existing DDR4 and is similar to LPDDR4.
~ $
```

Running the command prints the following:

```bash
~ $ sed 's/DDR/DNS/g' ddr4_vs_5
DNS5 is improvement to existing DNS4 and is similar to LPDNS4.
~ $
```

However, examining the first line printed above reveals that no changes have been written to the file itself.

```bash
~ $ head -1 ddr4_vs_5
DDR5 is improvement to existing DDR4 and is similar to LPDDR4.
~ $
```

The changes are written to the file, if one specifies option `-i`, in the `sed` command.

```bash
~ $ sed -i 's/DDR/DNS/g' ddr4_vs_5 && head -1 ddr4_vs_5
DNS5 is improvement to existing DNS4 and is similar to LPDNS4.
~ $
```

Deleting character\(s) is done by not giving it a replacement.

```bash
~ $ sed 's/improvement//g' ddr4_vs_5 | head -1
DNS5 is  to existing DNS4 and is similar to LPDNS4.
```

Notice the two white spaces between 'is' and 'to'. In order to only have one afterwards, one can do it like so:

```bash
~ $ sed 's/improvement //g' ddr4_vs_5 | head -1
DNS5 is to existing DNS4 and is similar to LPDNS4.
~ $
```

To delete every line, where a pattern is matched on, the user can use:

```bash
~ $ sed '/DDR/d' ddr4_vs_5





~ $
```

It left an empty file after running the above command. There was an occurrence of `DDR` on every line and every line was deleted.

---

`sed`

Using a different file 'seinfeld-characters', which has some empy lines, the task is to delete all empty files from the file. The file at the start:

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
```

Command and file after running sed:

- `-i` option to write changes to file.
- `^` and `$` are regex symbols in this case.
  - `^` matches the beginning of a line.
  - `$` matches the end of a line.
- `^$` matches start and end of a line, where nothing is between beginning and end of that line == it matches empty lines only.

```bash
~ $ sed -i '/^$/d' seinfeld-characters
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

#### Deleting Lines with `sed` \- 1

Removing the first line of a file using `sed`.

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
```


#### Deleting Lines with `sed` \- 2


- `sed '1d' FILE` delets the first line.
  - '2d', '3d' delets the second and third line respectively.
    - \'$n_{i}d$\' will remove line number $n_{i}$.
    - \'$n_{i},n_{j}d$\' will remove line number $n_{i} \text{ and } n_{j}$. ${i}, {j} \in L \text{ } \text { } {i} \ne {j} \text{ }  \forall i,j \in L$.  ${L}$being the set of all line index values in the file.
  - No `-i` was added, so changes only get output to **stdout (1)**

```bash
~ $ sed '1d' seinfeld-characters
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

#### Removing Certain Lines Using `sed`

Removing lines 1 and 2 of a file using `sed`.

Removing lines '1' and '2' can be done like illustrated above.

```bash
~ $ sed 1,2d seinfeld-characters
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

```bash
~ $ cat seinfeld-characters
Jerry Seinfeld, # This line is omitted in the above output.
Cosmo Kramer, # This line is omitted in the above output.
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

#### Replacing TAB with SPACE

The file uses tabs insted of spaces on the first three lines.

```bash
~ $ cat seinfeld-characters
Jerry	Seinfeld,
Cosmo	Kramer,
Eliane	Benes,
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

#### More Ways to use `sed`

Using `sed` with:
- `s/` tells it to substitute what comes after theforward slash.
- `\t/` tells it, that it has to look for usuallyinvisible TAB occurences. The 't' has to be escaped forit be recognised as a TAB by the command.
- ` ` (one space) means that it should replace TAB with SPACE.
- `/g` tells it to do the above for every occurences inthe file, not just the first one it matches.

```bash
~ $ sed 's/\t/ /g' seinfeld-characters # Replacing TAB with SPACE
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

#### Print Certain Lines to `stdout` 

Having a range of lines in a file printed to stdout.

The following prints lines 12 to 18 from the 'seinfeld-characters' file. Options specified are:
- `-n`
- `p`

```bash
~ $ sed -n 12,18p seinfeld-characters
J Peterman,
George Steinbrenner,
Uncle Leo,
David Puddy,
Justin Pit,
Kenny Bania
Uncle Leo,
```

#### Print all lines, except 12-18 from the file.

Using `d`

```bash
~ $ sed 12,18d seinfeld-characters
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
~ $
```

#### Inserting a new line 
Putting an empty line after each character's name.
Again, changes will not be written to the file without the `-i` options.

```bash
~ $ sed G seinfeld-characters
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

#### Limiting the lines `sed` will process.

One can limit the lines, which are processed by the `sed` command in a file. The excluded line or lines will not be processed by the `sed` command, like so:

*All occurences of 'Seinfeld', except for any on line number 8 are changed to 'GigaChad'. `nl` command is used before `sed`, to identify lines where 'Seinfeld ' occurs, so one line can be used as an exception for the `sed` command.*

```bash
~ $ nl seinfeld-characters | grep "Seinfeld"
     1	Jerry Seinfeld,
     8	Morty Seinfeld,
     9	Helen Seinfeld,
```

```bash
~ $  sed '8!s/Seinfeld/GigaChad/g' seinfeld-characters
Jerry GigaChad, # Line was changed.
Cosmo Kramer,
Eliane Benes,
George Costanza,
Newman Mailman,
Frank Costanza,
Estelle Costanza,
Morty Seinfeld, # Line was not changed (Index 8).
Helen GigaChad, # Line was changed.
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

<!---
Vim substitute  see screenshots.
-->

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












---
title: 'Learning Linux - Chapter 5: Section 5'
description: 'The `/etc/login.defs` file is described and the variables defined inside this file in terms of their definition and usage when running the `useradd` command.'
date: 2022-01-01 05:05:00
featured_image: 'mT68055%25%25--tYF_5__5jhhh5pls$0-G.jpeg'
gallery_images: 'YtOk89__87-kbtTGW$DD-L.jpeg'
accent_color: '#08877d'
---

# `chage` command in depth

**Learning Linux - Section 5.5**

The `/etc/login.defs` file is described and the variables defined inside this file in terms of their definition and usage when running the `useradd` command.

`chage` = 'change age' 

The command has the following important options. It is a command that is designed to be used for an individual user,
in the way it is shown here. In a corporate environment much this is automated, so one does not have to define values for each user that has to be created. Default values are used instead.


| Option | Description     | Example                                                                                      | Column No. in '/etc/shadow' |
|:------:|-----------------|----------------------------------------------------------------------------------------------|:---------------------------:|
|  `-m`  | MIN DAYS        | Minimum days between password changes                                                        |              4              |
|  `-M`  | MAX DAYS        | Maximum period, before user is forced to change his/her password                             |              5              |
|  `-d`  | LAST DAY        | The number of days, counting from 01/01/1970, where the most recent password change happened |              3              |
|  `-I`  | INACTIVE        | The number of days, after the password expires, that a account gets disabled                 |              7              |
|  `-E`  | EXPIRATION DATE | Number of days starting from 01/01/1970, where the account will be disabled                  |              8              |
|  `-W`  | PASS_WARN_AGE   | The number of days before a user's password expires, that a warning is given to him          |              6              |
| `User` | USERNAME        | The username                                                                                 |              1              |


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
| PASS_WARN_AGE   | 7               	 |     The number of days before a user's password expires, that a warning is given to him.     |
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
- Another option to make it more secure would be to make the values for uid harder to guess, using an algorithm to create pseudo random uid values for uid.
- The theoretical number of users that can be created is defined by the difference between `UID_MAX` and `UID_MIN`. In the above example a maximum of 59000 users could be created. This relationship between the upper and lower limits for the `UID` values and the theoretical number of users that can be created comes from the fact, that every single `uid` has to be uniq. This variable is a *unique key*.

### Recap - Structure of `/etc/shadow`
```
will:$6$.n.:17736:0:99999:7:::
[--] [----] [---] - [---] ----
|      |      |   |   |   |||+-----------> 9. Unused
|      |      |   |   |   ||+------------> 8. Expiration date
|      |      |   |   |   |+-------------> 7. Inactivity period
|      |      |   |   |   +--------------> 6. Warning period
|      |      |   |   +------------------> 5. Maximum password age
|      |      |   +----------------------> 4. Minimum password age
|      |      +--------------------------> 3. Last password change
|      +---------------------------------> 2. Encrypted Password
+----------------------------------------> 1. Username
```
**Graphic\:** [From linuxize](https://linuxize.com/post/etc-shadow-file/)

##### Creating a new user 'kate'

- First, a new group called *cyclists* is created by use of `groupadd`.
- Then, the user *kate* is created with command `useradd`, specifying several options.
  - `-g` makes her a member of group *cyclists*.
  - `-d` sets her shell environment to **bin/bash**.
  - `-c` Adds a description.
  - `-m -d` Sets her *'home directory'* *username*, separated by space.

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

#### Updating some initial values for 'kate'

##### Reading the default values in `/etc/shadow` for 'kate'

Below are the values from **/etc/shadow** for user *kate* after initialisation 
and changes to the default values using `chage` with various options. The ordered list shows the corresponding column numbers in the **/etc/shadow** file. 

3. Set by using\: `chage -d <username>` has a value of **18987**. It marks the date, the account password was created, counting the days since 01/01/1970 in this case till creation of the account.
4. `chage -m <username>` alters the value for minimum time period between password changes. Here, there is no minimum amount the user has to wait until they can change their password.
5. The default value for `chage -M <username>` during account creation is **99999** days. That means that the user never has to change their password.
6. The warning period `chage -W <username>` defaults to **7** days and is changed to **10**.
7. Is the option `chage -I <username>` that sets for how long the user account will still be active, after the password has not been updated within the time limit found in the value for **column 5.** and `chage -W <username>` as well.

```vim
kate:!!:18987:0:99999:7:::
```

##### Altering values for 'kate' in `/etc/shadow`

Values, that are changed for *kate*, are\:

4. The time span the user has to wait, until they can change their password went from **0** days to **5** days.
5. *Kate* now has to change her password at least every **90** days, prior she did not have to change it ever. The value was **99999** by default.
6. A warning was sent to kate, **7** days before the time period defined by `chage -M <username>` was over. Now she gets a warning, 10 days before that time period is over. Since `chage -M <username>` was set to **99999** `chage -W 7` would have never been triggered.

```bash
root * chage -m 5 -M 90 -W 10 -I 3 kate
root * grep "kate" /etc/shadow
kate:!!:18987:5:90:10:3::
root * 
```













---
title: 'Learning Linux - Chapter 5: Section 6'
description: 'The `sudo` command is explored in this section along with how to switch users, using the command line. Only basic commands are used, that are available in any Linux distribution and Unix based system.'
date: 2022-01-01 05:06:00
featured_image: 'mT68055%25%25--tYF_5__5jhhh5pls$0-G.jpeg'
gallery_images: 'YtOk89__87-kbtTGW$DD-L.jpeg'
accent_color: '#08877d'
---


# How to switch users and `sudo` access

**Learning Linux - Section 5.6**

The `sudo` command is explored in this section along with how to switch users, using the command line.
Only basic commands are used, that are available in any Linux distribution and Unix based system.

### How to switch users and `sudo` access

#### Commands covered

- `su - username`
- `sudo <command>`
- `visudo`

#### Relevant file

- **/etc/sudoers**

#### Routine commands to run after login into a *VM*

Since a virtual machine is used for all the sections and exercises, 
one should make sure that the following values are what they should be.

##### `whoami`: Which user am I?

```bash
~ $ whoami
tklein
~ $ 
```

##### `pwd`: What is my current absolute `path`?

```bash
~ $ pwd
/home/tklein
~ $ 
```

##### `hostname`: On which `host` am I currently?

```bash
~ $ hostname
localhost.localdomain
~ $ 
```

#### `su` and `sudo`

**Command:** `su - username` 

One enters the 'username' of the account one wants to become. If left blank,
it defaults to 'username' == `root`

Becoming user `root` and staying root until one decides to `exit` the root account,
is done like demonstrated below. One must have sufficient permissions to become root and know the password for the 
root user account.

```bash
~ $ su -
Password: 
Last login: Sun Dec 26 23:05:13 CET 2021 on pts/0
root * 
```
While root, one can change into any other `username`, without being prompted to enter that *username's* password.  

```bash
~ $ su -
Password: 
Last login: Mon Dec 27 09:56:48 CET 2021 on pts/0
root * su - kate
[kate@localhost ~]$ 
```

Exiting the root account again is done by entering `exit` after one's prompt.

```bash
root * exit
logout
~ $ whoami
tklein
~ $ 
```

**Command:** `sudo <command>`

The `sudo` command lets a user, who can not become `root` himself. It allows such a user
to run commands, that only user `root` can run usually, if they are in group `wheel` for example or in the **sudoers** file.

Two commands that can only be run by `root` are `dmidecode` and `fdisk -l`, to run these one has to 

```bash
~ $ dmidecode
# dmidecode 3.2
/sys/firmware/dmi/tables/smbios_entry_point: Permission denied
Scanning /dev/mem for entry point.
/dev/mem: Permission denied
~ $ fdisk -l
fdisk: cannot open /dev/sda: Permission denied
fdisk: cannot open /dev/mapper/centos-root: Permission denied
fdisk: cannot open /dev/mapper/centos-swap: Permission denied
~ $ 
```

One can add or change the permissions that a user has, to let them become root for example or
to let them run any command in the shell, if they are a member of group `wheel` by default. This 
group is by default listed in the file `visudo`.

##### Example

The example comes from a file that can be accessed by running `visudo` with `root` privileges.

```bash
## Allow root to run any commands anywhere
root    ALL=(ALL)       ALL
will    ALL=(ALL)       ALL # Only an example
## Allows people in group wheel to run all commands
%wheel  ALL=(ALL)       ALL
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL
```

###### `usermod -aG`

Adding account 'tklein' to group `wheel`

```bash
root * usermod -aG wheel tklein
root * 
```

###### Verification

- Using `id <username>` one gets all the groups the user is a member of.
- `grep "wheel" /etc/group` will print a line from the **/etc/group** file, to verify the changes.

```bash
root * id tklein
uid=1000(tklein) gid=1000(tklein) groups=1000(tklein),10(wheel)
root * grep "wheel" /etc/group
wheel:x:10:tklein
root * 
```

##### Retrying dmidecode and fdisk commands

After it was not able to run either `dmidecode` or `fdisk -l` using my user account *tklein*,
now it is possible to run `dmidecode` being part of group wheel:

###### `dmidecode`


```bash
[will@localhost ~]$ su - tklein
Password:
Last login: Mon Dec 27 15:20:49 CET 2021 on pts/1
~ $ whoami
tklein
~ $ sudo dmidecode
[sudo] password for tklein:
# dmidecode 3.2
Getting SMBIOS data from sysfs.
SMBIOS 2.5 present.
10 structures occupying 450 bytes.
Table at 0x3EFFD020.

Handle 0x0000, DMI type 0, 20 bytes
BIOS Information
	Vendor: innotek GmbH
	Version: VirtualBox
	Release Date: 12/01/2006
	Address: 0xE0000
	Runtime Size: 128 kB
	ROM Size: 128 kB
	Characteristics:
		ISA is supported
		PCI is supported
		Boot from CD is supported
		Selectable boot is supported
		8042 keyboard services are supported (int 9h)
		CGA/mono video services are supported (int 10h)
		ACPI is supported
		UEFI is supported
Handle 0x0001, DMI type 1, 27 bytes
Handle 0x0001, DMI type 1, 27 bytes
System Information
	Manufacturer: innotek GmbH
	Product Name: VirtualBox
	Version: 1.2
	Serial Number: 0
	UUID: 008f59e3-ffb4-5947-aaba-763e1257b612
	Wake-up Type: Power Switch
	SKU Number: Not Specified
	Family: Virtual Machine
Handle 0x0008, DMI type 2, 15 bytes

...
```

###### The `fdisk -l` command:

```bash
~ $ sudo fdisk -l
WARNING: fdisk GPT support is currently new, and therefore in an experimental phase. Use at your own discretion.

Disk /dev/sda: 10.7 GB, 10737418240 bytes, 20971520 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk label type: gpt
Disk identifier: 8C3022AF-D83D-4714-A904-26629F38B595


#         Start          End    Size  Type            Name
 1         2048       411647    200M  EFI System      EFI System Partition
 2       411648      2508799      1G  Microsoft basic
 3      2508800     20969471    8.8G  Linux LVM

Disk /dev/mapper/centos-root: 8376 MB, 8376025088 bytes, 16359424 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes


Disk /dev/mapper/centos-swap: 1073 MB, 1073741824 bytes, 2097152 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes

~ $
```





---
title: 'Learning Linux - Chapter 5: Section 7'
description: 'In this section, we look at how to monitor users, as a system administrator. We will cover `who`, `last`, `w`, `finger` and the `id` command.'
date: 2022-01-01 05:07:00
featured_image: 'mT68055%25%25--tYF_5__5jhhh5pls$0-G.jpeg'
gallery_images: 'YtOk89__87-kbtTGW$DD-L.jpeg'
accent_color: '#08877d'
---


# Monitoring Users

**Learning Linux - Section 5.7**


### How to monitor users


In this section, we look at how to monitor users, as a system administrator. We will cover `who`, `last`, `w`, `finger` and the `id` command.

#### Commands covered

- `who`
- `last`
- `w`
- `finger`
- `id`

#### Routine commands after login

After having logged in into the virtual machine, one runs, as always, the following commands:

```bash
Last login: Mon Dec 27 15:21:26 2021
~ $ whoami
tklein
~ $ pwd
/home/tklein
~ $ hostname
localhost.localdomain
~ $ 
```

#### `who`

- Tells one how many people are logged in at the time of running the command.


| Column | Example          |  
|--------|-------------------|  
| **Username** | kate                 |  
| **Terminal id for uid** |  :0      |  
| **Time logged in for uid** |   2019-03-10 14:33 (:0)     |
| **Hostname**				|	*win11.fritz.box*	|

```bash
~ $ who
tklein   tty1         2021-12-23 13:19
tklein   pts/0        2021-12-27 17:16 (win11.fritz.box)
tklein   pts/1        2021-12-27 15:20 (win11.fritz.box)
kate     pts/2        2021-12-27 18:16 (win11.fritz.box)
will     pts/3        2021-12-27 18:17 (win11.fritz.box)
~ $ 
```

`who` is oftentimes used, if the system is running slow and the system administrator wants to check who is logged in and how many are 
logged in.

#### `last`

`last` tells one everything about any user that has logged into the system, ever since the file **/var/log/wtmp** was 
created, by default.

```bash
DESCRIPTION
       Last  searches  back through the file /var/log/wtmp (or the file designated by the -f flag) and displays a list 
       of all users logged in (and out) since that file was created.  Names of users and tty's can be given, in which 
       case last will show only those entries matching the arguments.
       Names of ttys can be abbreviated, thus last 0 is the same as last tty0.
```

##### Sample output from running `last`

```bash
~ $ last | more
# User	 Terminal	 Hostname  	Most recent login  Time of logout + Time was onlline.
will     pts/3        imac2017.fritz.b Mon Dec 27 18:17   still logged in   
kate     pts/2        imac2017.fritz.b Mon Dec 27 18:16   still logged in   
tklein   pts/0        imac2017.fritz.b Mon Dec 27 17:16   still logged in   
tklein   pts/1        imac2017.fritz.b Mon Dec 27 15:20   still logged in   
tklein   pts/0        imac2017.fritz.b Mon Dec 27 08:53 - 16:53  (07:59)    
tklein   pts/0        imac2017.fritz.b Sun Dec 26 23:03 - 00:16  (01:12)    
tklein   pts/0        imac2017.fritz.b Sun Dec 26 15:21 - 17:48  (02:26)    
tklein   pts/1        imac2017.fritz.b Sun Dec 26 08:19 - 22:58  (14:38)    
tklein   pts/0        tobiass-imac.fri Sat Dec 25 12:37 - 09:49  (21:11)    
tklein   pts/0        tobiass-imac.fri Sat Dec 25 04:02 - 12:31  (08:28)    
tklein   pts/2        tobiass-imac.fri Sat Dec 25 02:37 - 04:38  (02:00)    
tklein   pts/1        192.168.178.101  Fri Dec 24 23:50 - 03:15  (03:25)    
tklein   pts/0        tobiass-imac.fri Fri Dec 24 23:49 - 03:15  (03:26)    
tklein   pts/0        tobiass-imac.fri Fri Dec 24 22:49 - 23:47  (00:58)    
tklein   pts/0        tobiass-imac.fri Fri Dec 24 20:34 - 22:48  (02:13)    
tklein   pts/0        tobiass-imac.fri Fri Dec 24 17:35 - 20:34  (02:58)    
tklein   pts/0        tobiass-imac.fri Fri Dec 24 16:54 - 17:17  (00:23)    
tklein   pts/1        tobiass-imac.fri Fri Dec 24 05:06 - 16:51  (11:45)    
tklein   pts/0        tobiass-imac.fri Fri Dec 24 02:10 - 05:27  (03:17)    
tklein   pts/0        tobiass-imac.fri Thu Dec 23 13:20 - 02:08  (12:47)    
tklein   tty1                          Thu Dec 23 13:19   still logged in   
reboot   system boot  3.10.0-1160.el7. Thu Dec 23 13:19 - 21:20 (4+08:01)   
tklein   tty1                          Thu Dec 23 13:17 - 13:19  (00:01)    
reboot   system boot  3.10.0-1160.el7. Thu Dec 23 13:17 - 21:20 (4+08:03)   

wtmp begins Thu Dec 23 13:17:01 2021
~ $ 
```

| Column No. 	| Description                                	     |             Example            	|
|:----------:	|--------------------------------------------------|:------------------------------:	|
|      1     	| **Username**                                   	 |              will              	|
|      2     	| **Terminal id**                                	 |              PTS/1             	|
|      3     	| **User's IP Address / Hostname**               	 |     169.254.245.11 / myvm1     	|
|      4     	| **Most Recent Login**                          	 |        Mon Dec 27 17:16        	|
|      5     	| **Most Recent Logout**                         	 | - 16:53 or '*still logged in*' 	|
|      6     	| **Timespan user was online most recently** 	     |         (07:59) (hh:mm)        	|

The following example shows how one can get column 1 alone printed in the console, have its values sorted and filter 
the unique values of column 1. The final pipe of the output will have the output printed with the line numbers for each unique 
entry of column 1.

*Note: awk only works in column 1 here. It separates columns by whitespace by default and the output of `last` is inconsistent 
in its column separation. Whitespace can be found in most of the values in its columns and so, one might have to add a different 
separator with the help of regular expressions to make this a CSV like table. It even prints wtmp at the bottom, because 
it aligns with the first column of the output.*

```bash
~ $ last | awk '{print $1}' | sort | uniq | nl
       
     1  kate
     2  reboot
     3  tklein
     4  will
     5  wtmp # Not part of the first column.
~ $ 
```

#### The `w`

The `w` command gives a similar output to the one `less` generates, but it gives more information, 
more detail compared to the latter.

##### Syntax for the `w` command

`w [OPTIONS] [USER]`  

##### The fields of the `w` table output

The fields found in the output of `w` are listed and described. An example for the values one can find in the output is given as well.

| Column     | Description                                                                                | Example         |
|------------|--------------------------------------------------------------------------------------------|-----------------|
| **USER**  | Prints the username                                                                        | *kate*          |
| **TTY**    | Name of the terminal used by the user                                                      | tty1            |
| **FROM**   | The hostname or IP from where the user is logged in                                        | 169.117.128.105 |
| **LOGIN@** | The time when the user logged in                                                           | 8:30            |
| **IDLE**   | The time since the user last interacted with the terminal,<br /> idle time                 | 7:19m           |
| **JCPU**   | The time used by all the processes attached to the tty                                     | 0.04s           |
| **PCPU**   | The time used by the user's current process.<br /> The one displayed in the **WHAT** field | 0.04s           |
| **WHAT**   | The user's current process and options/arguments                                           | w               |


##### `w` with no options or arguments

`w`

```bash
~ $ w
 23:01:40 up 4 days,  9:42,  5 users,  load average: 0.00, 0.01, 0.05
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
tklein   tty1                      Thu13    2days  0.04s  0.04s -bash
tklein   pts/0    imac2017.fritz.b 17:16    4.00s  0.07s  0.02s w
tklein   pts/1    imac2017.fritz.b 15:20    7:19m  0.08s  0.02s -bash
kate     pts/2    imac2017.fritz.b 18:16    4:45m  0.03s  0.03s -bash
will     pts/3    imac2017.fritz.b 18:17    4:44m  0.03s  0.03s -bash
~ $ 
```
###### `w` with the \[USER\] argument

`w tklein`

```bash
~ $ w tklein
 23:59:05 up 4 days, 10:39,  5 users,  load average: 0.00, 0.01, 0.05
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
tklein   tty1                      Thu13    2days  0.04s  0.04s -bash
tklein   pts/0    imac2017.fritz.b 17:16    1.00s  0.05s  0.00s w tklein
tklein   pts/1    imac2017.fritz.b 15:20    8:16m  0.08s  0.02s -bash
~ $ 
```


#### `finger`

`finger` is not part of the packages that come with a default **CentOS 7.9** installation.<br />
However it is a very powerful tool to have in one's arsenal when it comes to user monitoring. 
It can be installed easily, if one has *root privileges*.<br />
It can be installed using package manager **yum** like so:<br />
`yum install finger -y`

Somehow `finger` took the descriptions I added for users *kate* and *will* and just split them<br />
over the columns **Name** and **Office**. I added the descriptions to the `useradd` command. <br />
`useradd ... -c "User is a real cyclist, no ebike.`<br />
Looking up `man useradd` the answer is quickly found. `-c` is *currently* used as the field for the user's full name.<br />
That is what it says.

>        -c, --comment COMMENT
>           Any text string. It is generally a short description of the login,
>			and is currently used as the field for the user's full name.


```bash
~ $ finger
Login    Name                    Tty      Idle  Login Time   Office     Office Phone   Host
kate     User is a real cyclist  pts/2    6:38  Dec 27 18:16  no ebike.                (imac2017.fritz.box)
tklein   tklein                  tty1       2d  Dec 23 13:19           
tklein   tklein                  pts/0          Dec 27 17:16                           (imac2017.fritz.box)
tklein   tklein                  pts/1    9:12  Dec 27 15:20                           (imac2017.fritz.box)
will     His wife says           pts/3    6:37  Dec 27 18:17  that his                 (imac2017.fritz.box)
~ $ 
```

#### `id`

##### Syntax of the command

`id [username]`

The `id` command can be entered without any further arguments. Like that it will print information  
of the user that runs the command in the shell. See first line of the example for that.  
It will always display:
-The `uid`, the numerical, unique key that every user has. It is between **UID_MIN** and **UID_MAX**, as covered in 5.5.
- The `gid` is the numerical, unique representation of the **group**, that a user is a member of. Something like a user group.
- `groups` lists further groups and group ids of groups that the user is a member of.

```bash
~ $ id
uid=1000(tklein) gid=1000(tklein) groups=1000(tklein),10(wheel) context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
~ $ id will
uid=1005(will) gid=1005(golfers) groups=1005(golfers)
~ $ id kate
uid=1006(kate) gid=1007(cyclists) groups=1007(cyclists)
~ $ 
```











---
title: 'Learning Linux - Chapter 5: Section 8 & 9'
description: 'Section 8 explores how a system administrator can communicate with users, by use of native command line tools. The following Section 9 is all about Linux Account Authentication.'
date: 2022-01-01 05:08:09
featured_image: 'mT68055%25%25--tYF_5__5jhhh5pls$0-G.jpeg'
gallery_images: 'YtOk89__87-kbtTGW$DD-L.jpeg'
accent_color: '#08877d'
---


# Communicating with Users

**Learning Linux - Section 5.8**


### Communicating with users

Section 8 explores how a system administrator can communicate with users, by use of native command line tools.

#### Commands covered

- `users`
- `wall`
- `write`

#### `users`

The output of the command gives all currently online users. *kate* and *will* are logged in
and I am logged in as well (*tklein*).


```bash
~ $ users
kate tklein tklein tklein will
~ $ 
```


#### Use Case for `wall`

*In a situation where the system administrator (**admin**) has to shut down the system for some kind 
of maintenance, the users need to be notified that the system will be down for that maintenance period.

In this scenario, the `wall` command could come in handy, like so:


```bash
~ $ 
Broadcast message from tklein@localhost.localdomain (pts/0) (Tue Dec 28 02:53:50 2021):


Dear fellow employees, we got a maintenance break ahead of us. That means that 
the system will be down from 1:30PM until approximately 2:15PM EST. Please save
your work and be ready for the maintenance break! As always, I am your admin a
nd you can always reach me at 187 and admin@C.com

--- Klein
```


#### *write \<username\>*

This message appears on the terminal of all online users. On the other hand, if only a 
certain user is being addressed by a message, the command `write <username>` will do just that.
The user, in this case *kate* gets the message immediately after one hits 
**ENTER** followed by **CTRL + D**. **CTRL + D** is also how the message above, written using `wall`
gets sent. In the example below, *kate* replies to *tklein* using `write tklein` and entering her message afterwards.


```bash
~ $ write kate
Hello Kate, 

It looks like there is a lot of network traffic coming from your machine. 
Please stop scraping half the internet for your newest deep learning algorithm 
for face recognition. In the off hours I can find a time slot for you to do all 
that downloading. 
~ $ 
Message from kate@localhost.localdomain on pts/2 at 03:03 ...
Hello, upsie, did not activate the bandwith limit.
EOF
```

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>


# Linux Account Authentication

**Learning Linux - Section 5.9**


### Linux Account Authentication

How is account creation and authentication handled, in the case of large companies? 
In these large corporations there are thousands of employees and even more servers!
It is simply inefficient, if one tried to create a new user account manually on hundreds of servers 
for a new employee for example.

That is where Linux account authentication comes into play.

#### Types of accounts

- Types of accounts
  - Local account
  - Domain/Directory account

##### Local Accounts

For the `local account` a new user is added by running the commands covered in the previous 
sections. Commands like `useradd`, `groupadd`, `usermod -G`, `id [username]`, `grep <username> /etc/passwd`, `grep <username> /etc/shadow` 
`grep <username> /etc/group`, `chage`, `userdel` and `groupdel` to create a new user account, to assign the correct permissions to it, to create new a new group for example and to verify that everything was created correctly as well. This is on a per-user basis and offers very limited scaling!

##### Domain/Directory Accounts

The authentication works like this for domain and directory accounts:

1. User tries to log into the *client*, which is his current machine.
2. He enters his account credentials and these are sent to the *server*
3. The *server* checks whether this account is authenticated.
4. Given that the account is authenticated, the *server* authenticates the user who sent the request.
5. The user can log in on the client.














---
title: 'Learning Linux - Chapter 5: Section 10 & 11'
description: 'Sections 10 and 11 describe popular directory services and system utility commands.'
date: 2022-01-01 05:10:11
featured_image: 'mT68055%25%25--tYF_5__5jhhh5pls$0-G.jpeg'
gallery_images: 'YtOk89__87-kbtTGW$DD-L.jpeg'
accent_color: '#08877d'
---



# Overview and Comparison of Popular Directory Services

**Learning Linux - Section 5.10**



### Overview and Difference between Popular Directory Services

- Linux is mostly used in corporate environments, by developers and system administrators for example. One of the main reasons Linux is chosen in these scenarios, is its safety and performance it has over Windows for example. The user base is limited.
- Windows has a product called *Active Directory* for account authentication.
  - For example, facebook runs on Linux behind the scenes. However, a Windows user will not log into a Linux client when they log in, in their browser.
  - There a middle man is used, that handles the login process that is some kind of *Directory Service*.
- *IDM* = Identity Manager
  - Red Hat built this product for companies that have many Linux users, in order to deal with the great number of employees that have to log in for one service or another.
  - It runs on Linux and is used for large corporate environments.
- *WinBIND* = Used in Linux to communicate with Windows (Samba).
  - Samba came up with this 'addon', that lets Linux users authenticate themselves against Windows *Active Directory*.
  - Use case is also Widows *Active Directory* users, that have to authenticate against a Linux server.
- *OpenLDAP* (open source)
  - It is an open source alternative to *IDM* developed by Red Hat. *IDM* is shareware, while *OpenLDAP* is free.
- *IBM Directory Server*
  - Proprietary technology, developed by IBM.
- *JumpCloud*
  - Another directory service option.
- *LDAP* = Lightweight Directory Access Protocol
  - *LDAP* is a protocol and not a service.
  - It is needed to communicate to any *Directory Service* 

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

# System Utility Commands

**Learning Linux - Section 5.11**




### Commands covered

- `date`
- `uptime`
- `hostname`
- `uname`
- `which`
- `cal`
- `bc`

#### `date`

The `date` command returns information about the current date of the system. 
It returns the following information from left to right:


| Column No. | date             |
|:----------:|------------------|
| 1          | Day of the week  |
| 2          | Month            |
| 3          | Day of the month |
| 4          | Time             |
| 5          | Time zone        |
 | 6          | Year             |


```bash
~ $ date
Tue Dec 28 11:38:47 CET 2021
~ $ 
```


#### `uptime`

The `uptime` command gives information about the system. Namely about for how long it has been running in total, the number of currently online users and the **CPU** load. The **CPU** load is measured by looking at the average number of jobs in the system's *run queue* for 3 different time periods. The periods are 1, 5 and 15 minutes.


| Column No. | Data                                                    | Example                        |
|:----------:|---------------------------------------------------------|--------------------------------|
| 1          | Current System Time                                     | 11:37:00                       |
| 2          | Shows for how long the system has been running in total | up 4 days 22:33                |
| 3          | Number of Users currently logged into the Linux system  | 3 users                        |
| 4          | Average **CPU** load for 1, 5 and 15 minute period      | load average: 0.00, 0.01, 0.05 |


```bash
~ $ uptime
 11:52:44 up 4 days, 22:33,  3 users,  load average: 0.00, 0.01, 0.05
~ $ 
```

#### `hostname`

`hostname` tells one about the hostname of the Linux machine one is currently logged in.
`hostname` is used to verify, that one is *actually* logged into the right machine. This can be important to verify before running critical commands on the machine that one is logged in. 

```bash
~ $ hostname
localhost.localdomain
~ $ 
```


#### `uname`

`uname` gives very brief information about the operating system, that is running on the current machine.

##### Example


```bash
~ $ uname
Linux
~ $ 
```


###### `uname -a`


With the option `-a` one gets more information. In addition to the type of operating system (*Linux*), it prints more details 
about the operating system as one can see in the example below.


###### Example


```bash
~ $ uname -a
Linux localhost.localdomain 3.10.0-1160.el7.x86_64 #1 SMP Mon Oct 19 16:18:59 UTC 2020 x86_64 x86_64 x86_64 GNU/Linux
~ $ 
```


#### `which`

The structure of the command is `which [options] [--] programname [...]` and it tells one, as stated in the man pages of `which`:

> which - shows the full path of (shell) commands.

The command can be used for example with the following types of commands: `which [command]` `which [alias]` or `which [variable]`.

##### Example


```bash
~ $ which pwd
/usr/bin/pwd

~ $ which $HOME
/usr/bin/which: no tklein in (/home)

~ $ which vi
alias vi='vim'
        /usr/bin/vim
~ $ 
```


#### `cal`

From the man pages of `cal`, one learns that the syntax of the command looks like this: `cal [options] [[[day] month] year]`

`cal` simply prints a calendar, that looks like in the example below. It will take the system date as the current date.

##### Example

The tool is mainly intended to be used as a quick way to view a calendar in the terminal.


```bash
~ $ cal
    December 2021   
Su Mo Tu We Th Fr Sa
          1  2  3  4
 5  6  7  8  9 10 11
12 13 14 15 16 17 18
19 20 21 22 23 24 25
26 27 28 29 30 31

~ $ 
```


#### `bc`

`bc` = Binary calculator
It is a basic calculator, that lacks builtin functions like *factorial (n!)* or any `root` function. These functions can however be defined in a separate text file and can be imported like that over and over again.


```bash
~ $ bc
bc 1.06.95
Copyright 1991-1994, 1997, 1998, 2000, 2004, 2006 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type `warranty'. 
2^10
1024
5*10^6/120
41666
```



















---
title: 'Learning Linux - Chapter 5: Section 12'
description: 'This section introduces and explains the terms Application, Script, Process, Daemon, Thread and Job. These will be described in more detail in the following sections.'
date: 2022-01-01 05:12:00
featured_image: 'mT68055%25%25--tYF_5__5jhhh5pls$0-G.jpeg'
gallery_images: 'YtOk89__87-kbtTGW$DD-L.jpeg'
accent_color: '#08877d'
---


# Processes, Jobs and Scheduling

**Learning Linux - Section 5.12**


### Processes, Jobs and Scheduling 

This section introduces and explains the terms Application, Script, Process, Daemon, Thread and Job. These will be described in more detail in the following sections.

#### Terms covered

- **Application** syn. *Service*
- **Script**
- **Process**
- **Daemon**
- **Threads**
- **Job**

#### *Application*

An **Application** or service is a program, that runs on your machine. Applications are very common and a few examples for **Applications** are:

- NTP
- NFS
- rsyslog
- Apache
- RTRR
- Rsync
- top
- etc.

#### *Script*

A **script** can be a small application or a command, that is written down in a file containing the steps, that the scripts will follow when called. The script includes the algorithm, that explains step by step what the instance calling it has to do in order to execute the script. An example for a script is a shell script, these scripts can be sometimes identified by having the extension *.sh*. 
In the case of a *shell script*, what is written in the script is executed top to bottom, line by line.
An simple example for such a script is the following:

```shell
#!/bin/bash
echo -e " the command 'whoami' returns:\n"
whoami
mkdir -p /home/tklein/script-execution
exedir='/home/tklein/script-execution'
cd ${exedir}
cat /home/tklein/cars_are_best > ${exedir}/cars_are_still_best
echo -e "\nThe file 'cars_are_still_best' has that many lines:"
wc -l ${exedir}/cars_are_still_best
echo -e "^@\nFancy new Line, just sayin'^@\n"
cat ${exedir}/cars_are_still_best | nl
echo -e "^@\nFancy new Line, just sayin'^@\n"
echo 'Script executed successfully, bash out!'

```

Which returns the following output on the command line:

```bash
~ $ bash scripts/real_script.sh
 the command 'whoami' returns:

tklein

The file 'cars_are_still_best' has that many lines and its absolute path is:
5 /home/tklein/script-execution/cars_are_still_best

Fancy new Line, just sayin'

     1  Not just any text file.
     2  The secret car file.
     3  No CAPS, REALLY: This is good stuff.
     4  The faster the car, the quicker it covers distance.
     5  A V12 engine is a twelve-cylinder piston engine. 

Fancy new Line, just sayin'

Script executed successfully, bash out!
~ $ 
```



#### *Process*

An *application* for example generates a *process* with a unique **process id**.

##### Examples for *Process*/*Services* Commands  

- `systemctl` or `service`
  - `systemctl` is the new command on Red Hat 7/8 and replaces `service`
- `ps` lets the user see what *processes* are running on their Linux machine.
- `top` shows the user all *processes* with dependant *processes* and information regarding memory and **CPU** load.
- `kill` stops a *process* by terminating the *process id* or the *process*.
- `crontab` is used to schedule the executions of these *services*, *processes* or *applications* on the system.
  - When one of these is executed, it becomes a *job*.


#### *Daemon*

A *daemon* is a process, that runs continuously in the background. A common use for *daemons* are **updater**. These can for example send a **HTTP**  `GET request` and gets a **HTTP** `response` in return, telling it if there is a new firmware available for download from the server.



#### *Threads*

Every *process* could have multiple *threads* associated with it. A running *application* could have running multiple threads running in the background.

#### *Job*

A *job* or *workorder* runs a *service* or *process* at a scheduled time.

#### `at.`

`at.` is similar to `crontab` as it is used to schedule the execution of  *service*, *process* or *application*, the difference however is that it is only used to do this once. It is not used for reoccurring *jobs*.





---
title: 'Learning Linux - Chapter 5: Section 13'
description: 'The systemctl command is introduced in this section, as found in CentOS 7 / Red Hat 7. It describes and gives multiple examples of how it can be used.'
date: 2022-01-01 05:13:00
featured_image: 'mT68055%25%25--tYF_5__5jhhh5pls$0-G.jpeg'
gallery_images: 'YtOk89__87-kbtTGW$DD-L.jpeg'
accent_color: '#08877d'
---


# The `systemctl` command


**Learning Linux - Section 5.13**




### The `systemctl` Command

The `systemctl` command is introduced in this section, as found in CentOS 7 / Red Hat 7. It describes and gives multiple examples of how it can be used.


#### Overview


- The `systemctl` command is a new tool to control system services.
- It is found in CentOS 7 / Red Hat 7 and later.
- `systemctl` command replaces the `service` command.


#### Name, Syntax and Description


From the top of the man page (`man systemctl`), one gets an overview of the name and syntax (*synopsis*) of the `systemctl` command, along with a
short description of it.


```
systemctl - Control the systemd system and service manager

SYNOPSIS
systemctl [OPTIONS...] COMMAND [NAME...]

DESCRIPTION
systemctl may be used to introspect and control the state of the
"systemd" system and service manager. Please refer to systemd(1)
for an introduction into the basic concepts and functionality
this tool manages.
```


#### `systemctl` Output


The output, that the `systemctl` command generates is in row form.
Each row shows the values of the variable designated to it. The following
table lists the fields found in the output and describes the values for
each field. The table below was reproduced from the [Red Hat System Administrator's Guide](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html-single/system_administrators_guide/index).


<div class="table" id="tabl-Managing_Services_with_systemd-Services-Status">
    <div class="table-contents">
        <table class="lt-4-cols lt-7-rows">
            <colgroup>
                <col class="col_1" style="width: 50%; "><!--Empty-->
                <col class="col_2" style="width: 50%; "><!--Empty--></colgroup>
            <thead>
            <tr>
                <th align="left" id="idm140499344203312" scope="col" valign="top">Field</th>
                <th align="left" id="idm140499344202224" scope="col" valign="top">Description</th>
            </tr>
            </thead>
            <tbody>
            <tr>
                <td align="left" headers="idm140499344203312" valign="top"><p>
                    <code class="literal">Loaded</code>
                </p>
                </td>
                <td align="left" headers="idm140499344202224" valign="top"><p>
                    Information whether the service unit has been loaded, the absolute path to the unit file, and a note whether the unit is enabled.
                </p>
                </td>
            </tr>
            <tr>
                <td align="left" headers="idm140499344203312" valign="top"><p>
                    <code class="literal">Active</code>
                </p>
                </td>
                <td align="left" headers="idm140499344202224" valign="top"><p>
                    Information whether the service unit is running followed by a time stamp.
                </p>
                </td>
            </tr>
            <tr>
                <td align="left" headers="idm140499344203312" valign="top"><p>
                    <code class="literal">Main PID</code>
                </p>
                </td>
                <td align="left" headers="idm140499344202224" valign="top"><p>
                    The PID of the corresponding system service followed by its name.
                </p>
                </td>
            </tr>
            <tr>
                <td align="left" headers="idm140499344203312" valign="top"><p>
                    <code class="literal">Status</code>
                </p>
                </td>
                <td align="left" headers="idm140499344202224" valign="top"><p>
                    Additional information about the corresponding system service.
                </p>
                </td>
            </tr>
            <tr>
                <td align="left" headers="idm140499344203312" valign="top"><p>
                    <code class="literal">Process</code>
                </p>
                </td>
                <td align="left" headers="idm140499344202224" valign="top"><p>
                    Additional information about related processes.
                </p>
                </td>
            </tr>
            <tr>
                <td align="left" headers="idm140499344203312" valign="top"><p>
                    <code class="literal">CGroup</code>
                </p>
                </td>
                <td align="left" headers="idm140499344202224" valign="top"><p>
                    Additional information about related Control Groups (cgroups).
                </p>
                </td>
            </tr>
            </tbody>
        </table>
    </div>
</div>


#### Usage Examples


In this section several of the `systemctl` commands are run inside the shell and further explained. The basic syntax used in the examples, referring
to the information from the `man systemctl` output from above, is: `systemctl COMMAND [NAME...]`.
The commands covered, using the `firewalld` service are the following:

##### `start`, `stop` and `status`

```bash
systemctl start servicename.service (firewalld)
systemctl stop servicename.service (firewalld)
systemctl status servicename.service (firewalld)
```


###### Example: `systemctl status servicename.service`

The output of the `systemctl status servicename.service`
is explained in detail. The explanation follows the row-wise structure of the output of the command.

```bash
~ $ su -
Password: 
systemctl status firewalld.service
● firewalld.service - firewalld - dynamic firewall daemon
   Loaded: loaded (/usr/lib/systemd/system/firewalld.service; enabled; vendor preset: enabled)
   Active: active (running) since Sun 2022-01-16 16:38:24 CET; 5h 54min ago
     Docs: man:firewalld(1)
 Main PID: 796 (firewalld)
   CGroup: /system.slice/firewalld.service
           └─796 /usr/bin/python2 -Es /usr/sbin/firewalld --nofork --nopid

Jan 16 16:38:23 192.168.178.196 systemd[1]: Starting firewalld - dynamic firewall daemon...
Jan 16 16:38:24 192.168.178.196 systemd[1]: Started firewalld - dynamic firewall daemon.
Jan 16 16:38:25 192.168.178.196 firewalld[796]: WARNING: AllowZoneDrifting is enabled. This is considered an insecur... now.
Hint: Some lines were ellipsized, use -l to show in full.
root * 
```

The output tells one the following about the status of the service `firewalld`:

- The service is loaded (**LOAD**).
  - That tells one, that the configuration file of the `firewall` service is loaded.
  - From the line above it can be concluded, that `systemctl` can reach and read that configuration file.
  - The configuration file is located at: '/usr/lib/systemd/system/firewalld.service'
- `firewalld` is loaded.
  - A loaded service will start automatically upon any kind of system startup.
- The service is **ACTIVE**.
  - It is currently running.
  - It has been running since *Sun 2022-01-16 16:38:24 CET*
  - Time since start is 5h 54min.
- The manual for `firewalld` can be opened with the command `man firewalld(1)`.
- It has the **PID** 796 (*processid*).
- The control groups (**CGroup**), showing higher level unit hierarchy. This is part of resource management, see [here](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/resource_management_guide/chap-introduction_to_control_groups) for detailed information.
- The last 3 lines give a brief history of the command. It is a log.

###### Example: `systemctl stop servicename.service`

In this example, the `firewalld` unit is stopped and its status
is checked afterwards, by running `systemctl status firewalld.service`

```bash
~ $ su -
Password: 
Last login: Mon Jan 17 13:03:17 CET 2022 on pts/0
root * systemctl stop firewalld.service
root * systemctl status firewalld.service
● firewalld.service - firewalld - dynamic firewall daemon
   Loaded: loaded (/usr/lib/systemd/system/firewalld.service; enabled; vendor preset: enabled)
   Active: inactive (dead) since Tue 2022-01-18 05:10:26 CET; 21s ago
     Docs: man:firewalld(1)
  Process: 23277 ExecStart=/usr/sbin/firewalld --nofork --nopid $FIREWALLD_ARGS (code=exited, status=0/SUCCESS)
 Main PID: 23277 (code=exited, status=0/SUCCESS)

Jan 18 05:10:02 vm8 systemd[1]: Starting firewalld - dynamic firewall daemon...
Jan 18 05:10:02 vm8 systemd[1]: Started firewalld - dynamic firewall daemon.
Jan 18 05:10:02 vm8 firewalld[23277]: WARNING: AllowZoneDrifting is enabled. T...w.
Jan 18 05:10:25 vm8 systemd[1]: Stopping firewalld - dynamic firewall daemon...
Jan 18 05:10:26 vm8 systemd[1]: Stopped firewalld - dynamic firewall daemon.
Hint: Some lines were ellipsized, use -l to show in full.
```


###### Example: `systemctl start servicename.service`


In this example, the `firewalld` unit is started again and its status
afterwards is checked, by running `systemctl status firewalld.service`
```bash
root * systemctl start firewalld.service
root * systemctl status firewalld.service
● firewalld.service - firewalld - dynamic firewall daemon
   Loaded: loaded (/usr/lib/systemd/system/firewalld.service; enabled; vendor preset: enabled)
   Active: active (running) since Tue 2022-01-18 05:11:30 CET; 3s ago
     Docs: man:firewalld(1)
 Main PID: 23467 (firewalld)
   CGroup: /system.slice/firewalld.service
           └─23467 /usr/bin/python2 -Es /usr/sbin/firewalld --nofork --nopid

Jan 18 05:11:30 vm8 systemd[1]: Starting firewalld - dynamic firewall daemon...
Jan 18 05:11:30 vm8 systemd[1]: Started firewalld - dynamic firewall daemon.
Jan 18 05:11:31 vm8 firewalld[23467]: WARNING: AllowZoneDrifting is enabled. T...w.
Hint: Some lines were ellipsized, use -l to show in full.
root * 
```


##### `disable` & `enable`

While `systemctl stop servicename.service` and  `systemctl start servicename.service`
stop and start a service immediately after execution, the commands
`systemctl disable servicename.service` and `systemctl enable servicename.service`
will do different things compared with `stop` and `start` respectively.

Enable will create hooks for the unit specified in the `systemctl enable...`
command in relevant directories/files, so that the unit will start on boot
automatically or when certain hardware is connected. There is a multitude of possible
triggers one can specify, that will cause the specified unit to start its service.
The trigger has to be specified in the *unit file* of the unit to be enabled.

Similarly, the `systemctl disable...` command will keep a unit from automatically starting,
after a specified trigger or triggers has or have occurred. Enable and disable are like toggles,
a unit can be only enabled or disabled and if currently enabled, it can only be
disabled and vice versa. 

Examples for these two commands follow below.

```bash
systemctl disable servicename.service
systemctl enable servicename.service
```

###### `systemctl disable servicename.service`

One can see, that the `firewalld` service is still active, after it has
been disabled. It is still loaded, however it is mentioned in the output, that it is disabled!

```bash
root * systemctl disable firewalld.service
Removed symlink /etc/systemd/system/multi-user.target.wants/firewalld.service.
Removed symlink /etc/systemd/system/dbus-org.fedoraproject.FirewallD1.service.
root * systemctl status firewalld.service
● firewalld.service - firewalld - dynamic firewall daemon
   Loaded: loaded (/usr/lib/systemd/system/firewalld.service; disabled; vendor preset: enabled)
   Active: active (running) since Tue 2022-01-18 05:11:30 CET; 1h 48min ago
     Docs: man:firewalld(1)
 Main PID: 23467 (firewalld)
   CGroup: /system.slice/firewalld.service
           └─23467 /usr/bin/python2 -Es /usr/sbin/firewalld --nofork --nopid

Jan 18 05:11:30 vm8 systemd[1]: Starting firewalld - dynamic firewall daemon...
Jan 18 05:11:30 vm8 systemd[1]: Started firewalld - dynamic firewall daemon.
Jan 18 05:11:31 vm8 firewalld[23467]: WARNING: AllowZoneDrifting is enabled. T...w.
Hint: Some lines were ellipsized, use -l to show in full.
root * 
```


###### `systemctl enable servicename.service`

Vice versa, enabling the `firewalld` service again does not change anything in terms of it being loaded and active. However, in the **Loaded** row, one can see that it is now
enabled again.


```bash
root * systemctl enable firewalld.service
Created symlink from /etc/systemd/system/dbus-org.fedoraproject.FirewallD1.service to /usr/lib/systemd/system/firewalld.service.
Created symlink from /etc/systemd/system/multi-user.target.wants/firewalld.service to /usr/lib/systemd/system/firewalld.service.
root * systemctl enable firewalld.service
root * systemctl status firewalld.service
● firewalld.service - firewalld - dynamic firewall daemon
   Loaded: loaded (/usr/lib/systemd/system/firewalld.service; enabled; vendor preset: enabled)
   Active: active (running) since Tue 2022-01-18 05:11:30 CET; 6h ago
     Docs: man:firewalld(1)
 Main PID: 23467 (firewalld)
   CGroup: /system.slice/firewalld.service
           └─23467 /usr/bin/python2 -Es /usr/sbin/firewalld --nofork --nopid

Jan 18 05:11:30 vm8 systemd[1]: Starting firewalld - dynamic firewall daemon...
Jan 18 05:11:30 vm8 systemd[1]: Started firewalld - dynamic firewall daemon.
Jan 18 05:11:31 vm8 firewalld[23467]: WARNING: AllowZoneDrifting is enabled. This is cons...ow.
Hint: Some lines were ellipsized, use -l to show in full.
root * 
```

##### `restart` & `reload`

`systemctl restart` and `systemctl reload` are two important commands to
understand.

`systemctl restart` will shut down the specified unit and then immediately
start it back up again. The downtime is minimized. It will also restart a
currently powered off unit, unless the restart statement is replaced by
`try-restart`. This option will only restart a running unit and not a powered
off one.

`systemctl reload` is only supported by some system services and will be ignored
all together by ones that don't support it.
It lets the user change its configuration files and reload the unit to use the
updated configuration files without stopping its service at all. This can be a
great feature for *always online services*, such as web servers.

```bash
systemctl restart servicename.service
systemctl reload servicename.service
```

###### `systemctl --all`

The `systemctl --all` will list all units in the system's registry.
Here it was used to list all units, so that the one called `mariadb`
would be found using the `grep "maria"` with piped input from
`systemctl --all`.

```bash
root * systemctl --all | grep "maria"
  mariadb.service 
                  active   running   MariaDB database server
root * 
```


###### `systemctl restart servicename.service`

Restarting the `mariadb` unit like so:

```bash
root * systemctl restart mariadb.service
root * systemctl status mariadb.service
● mariadb.service - MariaDB database server
   Loaded: loaded (/usr/lib/systemd/system/mariadb.service; enabled; vendor preset: disabled)
   Active: active (running) since Tue 2022-01-18 12:10:45 CET; 18s ago
  Process: 24184 ExecStartPost=/usr/libexec/mariadb-wait-ready $MAINPID (code=exited, status=0/SUCCESS)
  Process: 24147 ExecStartPre=/usr/libexec/mariadb-prepare-db-dir %n (code=exited, status=0/SUCCESS)
 Main PID: 24182 (mysqld_safe)
   CGroup: /system.slice/mariadb.service
           ├─24182 /bin/sh /usr/bin/mysqld_safe --basedir=/usr
           └─24347 /usr/libexec/mysqld --basedir=/usr --datadir=/var/lib/mysql --plugin-dir=...

Jan 18 12:10:43 vm8 systemd[1]: Starting MariaDB database server...
Jan 18 12:10:43 vm8 mariadb-prepare-db-dir[24147]: Database MariaDB is probably initialize...e.
Jan 18 12:10:43 vm8 mariadb-prepare-db-dir[24147]: If this is not the case, make sure the ...r.
Jan 18 12:10:43 vm8 mysqld_safe[24182]: 220118 12:10:43 mysqld_safe Logging to '/var/log/...g'.
Jan 18 12:10:43 vm8 mysqld_safe[24182]: 220118 12:10:43 mysqld_safe Starting mysqld daemo...sql
Jan 18 12:10:45 vm8 systemd[1]: Started MariaDB database server.
Hint: Some lines were ellipsized, use -l to show in full.
root * 
```

In the output one can see, that the unit has been running for **18s** only and thus
the restart was successful, since it is up and active again.


###### `systemctl reload servicename.service`

As mentioned earlier, not all units support the `systemctl reload servicename.service`
command and so is the case for the `mariadb` service, as seen in the following
output:

```bash
root * systemctl reload mariadb.service
Failed to reload mariadb.service: Job type reload is not applicable for unit mariadb.service.
See system logs and 'systemctl status mariadb.service' for details.
root * 
```

A service which supports the `reload` command is the `httpd`
service. One can reload it like so:

```bash
root * systemctl reload httpd.service
```

That is the end for this section.
