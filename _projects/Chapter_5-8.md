---
title: 'Communicating with Users'
subtitle: 'Learning Linux - Section 5.8'
date: 2021-12-29 00:00:00
description: 'This article covers some of the essential commands used in any Linux distribution. Vim text editor was used and CentOS 7 was the OS used in this series. It was setup as command line only virtual machine and accessed through ssh. There are 8 Sections in total.'
featured_image: bash-ga254901e3_1280.png
gallery_images: Bash_GNOME_Terminal_screenshot.png
accent_color: '#08877d'
---

### Communicating with users

#### Commands covered

- `users`
- `wall`
- `write`

#### *users*

The output of the command gives all currently online users. *kate* and *will* are logged in
and I am logged in as well (*tklein*).


```bash
~ $ users
kate tklein tklein tklein will
~ $ 
```


#### Use Case for *wall*

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
