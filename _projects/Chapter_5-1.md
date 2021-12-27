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
  - `d` \- delete
  - `:q!` \- quit vi without saving recent changes
  - `:wq` \- quit and save

##### Writing and exiting a file

There are several options for how to accomplish this\:


1. While in insert mode\:
   1. Hit `Esc` \> `:` \> type\: `wq` on the command line.
   2. Hit `Esc` \> Hit (capital) `Z` `Z` and the file will be saved and vi quits.