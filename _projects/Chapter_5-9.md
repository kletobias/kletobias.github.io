---
title: 'Linux Account Authentication'
subtitle: 'Learning Linux - Section 5.9'
date: 2021-12-31 00:00:00
description: 'This article covers some of the essential commands used in any Linux distribution. Vim text editor was used and CentOS 7 was the OS used in this series. It was setup as command line only virtual machine and accessed through ssh. There are 8 Sections in total.'
featured_image: 'mT68055%25%25--tYF_5__5jhhh5pls$0-G.jpeg'
gallery_images: 'YtOk89__87-kbtTGW$DD-L.jpeg'
accent_color: '#08877d'
---

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