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


