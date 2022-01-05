---
title: 'sed command'
subtitle: 'Learning Linux - Section 5.3'
date: 2021-11-28 00:00:00
description: 'This article covers some of the essential commands or concepts used in any Linux distribution.'
featured_image: bash-ga254901e3_1280.png
gallery_images: Bash_GNOME_Terminal_screenshot.png
accent_color: '#08877d'
---

### Introduction

The Vim text editor was used and CentOS 7.4 was the distribution installed on the virtual machine in this series. It was setup as a command line only virtual machine and accessed through ssh. There are 8 Sections in total.

<!---Gallery is used, when listing the articles, featured is the image placed at the top of the article.
-->

### *sed* command

- `sed` replaces a string in a file with a new string.
- It can be used to find and delete a line of a file. Use cases are\:
  - Remove empty lines.
  - Remove the first line or `n` lines.
  - Replace tabs with spaces.
  - Show defined lines from a file.
  - Substitute \(replace) within vi editor.
  - And much more...

#### `sed 's/DDR/DNS/g' FILE`

- Like this, the command does\:
  - `s` substitute
  - `DDR` with `DNS`
	- `g` - do this for all matches in the `FILE` /(`g` == global).
	- It will not write the above changes to the file by default and will only show them on screen.
	- Changes are written, if `-i` is added.


##### Example

The this text file is used in the following examples.

```vim
~ $ cat ddr4_vs_5
DDR5 is improvement to existing DDR4 and is similar to LPDDR4.

While DDR4 DIMMs (memory stick) are 64 bits (72 bits with ECC, so called buffered or registered) DDR5 moved to 2 x 32 bits or 2 x 40 bits for ECC. Btw LPDDR4 is 2 x 16 bits. DDR5 DIMM has two separate 32 bit channels, like two DDR4 DIMMs - single DDR5 DIMM is dual channel.

Additional improvement is number of burst transfers. While DDR4 is 4 or 8, LPDDR4 16 or 32, DDR5 increased to 16. By doubling bursts DDR5 despite 32 bits achieves DDR4 speeds. Btw in x86 CPU (and others too) cache line is 64 bytes what corresponds to DDR4 64 bits and 8 transfers.

Operating voltage is reduced from 1.2V to 1.1V what reduces power consumption, eg LPDDR4 is 1V. Additional features are added which speed up DDR5 further, eg number of banks, hidden refresh, etc.

Also memory sizes are increased. DDR4 per DIMM is 32GB while DDR5 increases this to 64GB and further.
Additionally transfer speeds are increased. Latest DDR4 is 3200/3600 (originally 2133 or 2166) while DDR5 starts at 4800, followed by 5200, 6000 and even 10000. Of course, latencies, famous CL, is also higher cause internally tech cannot improve too much. Eg DDR4 3200 has CL 16 what is 10 ns while DDR5 4800 is 34 what is 14 ns. There are more expensive CL 30 DIMMs. So, no big differences but compensated with longer bursts and higher transfer speeds.

At the end DDR5 is bit faster but is also way more expensive.
~ $
```

Reading the first line before running `sed` on the file\:

```bash
~ $ head -1 ddr4_vs_5
DDR5 is improvement to existing DDR4 and is similar to LPDDR4.
~ $
```

Running the command prints the following\:

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

Notice the two white spaces between 'is' and 'to'. In order to only have one afterwards, one can do it like so\:

```bash
~ $ sed 's/improvement //g' ddr4_vs_5 | head -1
DNS5 is to existing DNS4 and is similar to LPDNS4.
~ $
```

To delete every line, where a pattern is matched on, the user can use\:

```bash
~ $ sed '/DDR/d' ddr4_vs_5





~ $
```

It left an empty file after running the above command. There was an occurrence of `DDR` on every line and every line was deleted.

---

#### Deleting empty lines using *sed*

Using a different file 'seinfeld-characters', which has some empy lines, the task is to delete all empty files from the file. The file at the start\:

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

Command and file after running sed\:

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

#### Removing the first line of a file using *sed*

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

#### Removing lines 1 and 2 of a file using *sed*

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

Using `sed` with\:
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

#### Having a range of lines in a file printed to stdout


The following prints lines 12 to 18 from the 'seinfeld-characters' file. Options specified are\:
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

#### Putting an empty line after each character\'s name

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

#### Limiting the lines *sed* will process.

One can limit the lines, which are processed by the `sed` command in a file. The excluded line or lines will not be processed by the `sed` command, like so\:

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
