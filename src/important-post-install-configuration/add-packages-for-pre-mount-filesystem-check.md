---
date: 2022-04-28
title: "Add packages for pre-mount filesystem check"
tags: ["alpine","howtos","docs","linux","sysadmin-devops"]
series: ["docs4web","alpine-linux-local-server"]
---

# Add packages for pre-mount filesystem check

## Overview

Where possible it is a best practise to check your filesystem before mounting them (especially read-write) to ensure you are not working with a corrupted (and further damaging a) filesystem.

## (Re)install the filesystem tools you need

If you are following the recommendation to operate as non-root, the only thing to remember is to 'become root' (e.g. `doas`, `sudo`, or `su`) when executing the `apk add` commands, when following the [filesystem tool install guide from the install process](../server-install-config/create-semi-data-install/add-and-use-filesystem-tools.md).

Enable localmount on default runlevel
--------------------------------------

    doas rc-update add localmount default

## Don't forget to commit your changes

Otherwise they will be lost on reboot.

```shell
doas lbu commit
```
