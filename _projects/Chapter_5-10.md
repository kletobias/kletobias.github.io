---
title: 'Overview and Comparison of Popular Directory Services'
subtitle: 'Learning Linux - Section 5.10'
date: 2022-01-06 00:00:00
description: 'In this Section we look at the difference between some of the popular Directory Services out there. E.g. *Active Directory*, *LDAP*, *IDM*, *WinBIND*, *OpenLDAP*.'
featured_image: bash-ga254901e3_1280.png
gallery_images: Bash_GNOME_Terminal_screenshot.png
accent_color: '#08877d'
---

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