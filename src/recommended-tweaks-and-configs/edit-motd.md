---
date: 2022-04-28
title: "Edit message of the day (MOTD)"
tags: ["alpine","howtos","linux","sysadmin-devops"]
series: ["docs4web","alpine-linux-local-server"]
description: "The default MOTD is potentially confusing, and is annoying in any event, once you have set up your system."
summary: "The default MOTD is potentially confusing, and is annoying in any event, once you have set up your system."
---

## Overview

The existing message of the day (MOTD) includes:

```plaintext
You can setup the system with the command: setup-alpine

You may change this message by editing /etc/motd.
```

Which is potentially confusing, and is annoying in any event, once you have set up your system. Fortunately changing it is easy.

## Configure '/etc/motd'

Simply execute:

``` shell
doas vi /etc/motd
```

Edit or replace the plaintext message here, save, and exit.

## Commit your changes

If you have been following along and applying this guide's recommendations:

``` shell
doas lbu commit
```
