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

