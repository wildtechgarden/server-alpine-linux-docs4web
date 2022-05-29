---
date: 2022-04-28
title: Create a non-root admin user
tags: ["alpine","configuration","docs","hosting","linux","security","self-host","sysadmin-devops"]
series: ["docs4web","alpine-linux-local-server"]
---

# Create a non-root admin user

## Avoid operating as root, where possible

It is generally considered an administrative best practise to avoid logging in and/or operating with elevated privileges, to the extent reasonable to do so. Therefore one needs a user is not root for performing most operations, but which can gain elevated access when required. In addition if, as recommended, one prevents root login over SSH one needs a user than one can SSH into and gain temporary elevated privileges. (Assuming a remotely accessed system, of course).

## Create a new user

``` shell
adduser -g ",,," newadmin newadmin
```

## Add doas or sudo

`sudo` is the traditional tool, `doas` comes from the *BSD world; both give elevated access. Discussing the relative merits is out of scope here, but we will use `doas` in our examples.

``` shell
apk add doas
```

OR

``` shell
apk add sudo
```

## doas: allow your admin user to 'become root'

Add your `newadmin` user as a `doas` user. Edit `/etc/doas.d/doas.conf` so that it contains:

```shell
permit newadmin
```

## Login as new user and test access

1. In a new virtual terminal (e.g via `Ctrl-Alt-F2`) login at the `login` prompt as your `newadmin` user or start a new SSH session as `newadmin`.
2. Execute `doas ls -al /root`
3. You should see the directory listing for `/root` which is owned and readable only by the `root` user.

## Don't forget to commit your changes

Otherwise they will be lost on reboot.

```shell
doas lbu commit
```

## Useful links

<https://wiki.alpinelinux.org/wiki/Setting_up_a_new_user>
