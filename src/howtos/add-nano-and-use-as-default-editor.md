---
date: 2022-04-28
title: "Add nano and use as default editor"
tags: ["alpine","howtos","docs","linux","sysadmin-devops"]
series: ["docs4web","alpine-linux-local-server"]
description: "For many users `vi` (the default editor for Alpine) is difficult and confusing to use."
summary: "For many users `vi` (the default editor for Alpine) is difficult and confusing to use."
---

## Overview

For many users `vi` (the default editor for Alpine) is difficult and confusing to use. Even if that is not the case for you, if you find it helpful to have the same experience as others you wish to help, you might implement this for your own use as well. \[_AUTHOR's NOTE_: I am guilty of _not_ doing this.]

As usual, commands below are to be executed as root.

## Install nano

``` shell
apk add nano
```

## Add a profile snippet to make nano the default editor

This change will apply to 'sh' (ask/bash/dash/etc) shells that are login shells, or sub-shells of a login shell. That means you will need to logout and log back in to see the effects of enabling this (or conversely disabling it).

Create `/etc/profile.d/default_editor.sh` with the following contents:

```shell
EDITOR=nano
export EDITOR
```
