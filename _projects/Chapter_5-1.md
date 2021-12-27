---
title: 'Learning Linux - Section 5.1'
subtitle: 'Linux Text Editors'
date: 2021-12-27 00:00:00
description: 'This article covers some of the essential commands used in any Linux distribution. CentOS 7 was the OS used in this series. It was setup as command line only virtual machine and accessed through ssh.'
featured_image: 80sterminal.png
gallery_images: Bash_GNOME_Terminal_screenshot.png
accent_color: '#4C60E6'
---

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

#### Introduction to vi editor

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

Moving the cursor inside of a text file in vi\:
- Moving up one line at a time\: `k`
- Moving down one line at a time\: `j`
- Moving to the left, one character at a time\: `h`
- Using `a` while in normal mod advances the cursor onecharacter and switches to `-- INSERT --` mode.
- A variation of pressing `a` is pressing `SHIFT + a`.This will advance the cursor to the end of the current line and change to `-- INSERT --` mode.
- `SHIFT + h` will move the cursor to the beginning of thefile, if pressed in normal mode.
- Using `o` lets the user create a new line just below thecursor and automatically changes the mode to `-- INSERT -`. The cursor is placed on the newly created line and one can start writing on the new line.

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

Hitting 'r', followed by 's', replaces 'h' with 's'.

```vim
No CAPS, REALLY: This is good stuff.
```

##### Moving around the file and manipulating text

- Using `o` lets the user create a new line just below the cursor and automatically changes the mode to `-- INSERT --`. The cursor is placed on the newly created line and one can start writing on the new line.

##### Searching inside a text file


