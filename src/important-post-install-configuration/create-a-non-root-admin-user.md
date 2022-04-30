---
date: 2022-04-28
title: Create a non-root admin user
tags: ["alpine","configuration","docs","hosting","linux","security","self-host","sysadmin-devops"]
series: ["docs4web","alpine-linux-local-server"]
---

# Create a non-root admin user

### Avoid operating as root, where possible

It is generally considered an administrative best practise to avoid logging in and/or operating with elevated privileges, to the extent reasonable to do so. Therefore one needs a user is not root for performing most operations, but which can gain elevated access when required. In addition if, as recommended, one prevents root login over SSH one needs a user than one can SSH into and gain temporary elevated privileges. (Assuming a remotely accessed system, of course).

Create a new user
-----------------

    adduser -g "Daniel F. Dickinson - Admin,,," newadmin newadmin # Obiously use your name or pseudonym hereu

Add doas or sudo
----------------

``sudo`` is the traditional tool, `doas` comes from the *BSD world; both give elevated access. Discussing the relative merits is out of scope here, but we will use `doas` in our examples.

    apk add doas

OR

    apk add sudo

doas: allow your admin user to 'become root'
------------------------------------------------------

TBD (group wheel)

Login as new user and test access
-----------------------------------------

TBD
