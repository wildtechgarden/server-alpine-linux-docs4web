---
date: 2022-04-28
title: "Add tmux"
tags: ["alpine","howtos","docs","linux","sysadmin-devops"]
series: ["docs4web","alpine-linux-local-server"]
description: "Tmux is a handy tool that gives the ability to have multiple (text) windows in a single terminal session, as well as persisting your session in case of disconnect."
summary: "Tmux is a handy tool that gives the ability to have multiple (text) windows in a single terminal session, as well as persisting your session in case of disconnect."
---

## Overview

Tmux is a handy tool that gives the ability to have multiple (text) windows in a single terminal session. In addition, if you get disconnected from the terminal (e.g. an SSH session drops out), when you log back in, you can attach back to the same session. This is particularly handy when you issue command that takes longer to complete than expected.

[Tmux does much more than this, and you probably ought to read about it](https://github.com/tmux/tmux/wiki).

## Install

``` shell
doas apk add tmux
```

Commit your changes

```shell
doas lbu commit
```
