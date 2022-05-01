---
date: 2022-04-28
title: "Add packages for pre-mount filesystem check"
tags: ["alpine","howtos","docs","linux","sysadmin-devops"]
series: ["docs4web","alpine-linux-local-server"]
---

# Add packages for pre-mount filesystem check

## Overview

TBD

Install vfat (fat32) and ext4 checkers
--------------------------------------

    apk add dosfstools \
     e2fsprogs \
     dosfstools-doc # Optional if you don't need/want the man page or other docs \
     e2fsprogs-docs # Likewise

Enable localmount on boot and default runlevels
-----------------------------------------------

    rc-update add localmount boot default
