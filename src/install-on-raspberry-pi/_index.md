---
date: 2022-04-29
title: Use Alpine Linux on Raspberry Pi as a server
tags: ["alpine","linux","self-host","sysadmin-devops","raspberry-pi"]
series: ["docs4web","alpine-linux-local-server"]
description: "Raspberry Pi-specific notes for preparing and installing Alpine Linux"
summary: "Raspberry Pi-specific notes for preparing and installing [Alpine Linux](https://alpinelinux.org)"
---

## Special Notes

**NOTE:** For boot to succeed `/media/mmcblk0p1/usercfg.txt` must exist. See [kernel parameters and device-tree settings](../kernel-and-hardware-notes/guides-for-setting-kernel-parameters.md#raspberry-pi) for information on what you can set in that file. A blank file is sufficient to allow booting, however.

## Guides

[Creating initial boot media](creating-initial-boot-media/_index.md)

[Server install and configure](../server-install-config/_index.md)

[Hardware-specific tweaks and configuration](../kernel-and-hardware-notes/hardware-specific-tweaks-configs.md)

## Existing Documentation

There are guides that are a bit of a mess on the [Alpine wiki](https://wiki.alpinelinux.org/wiki/Main_Page). I suppose so are these, by they are _my_ mess.

<https://wiki.alpinelinux.org/wiki/Raspberry_Pi>  
<https://wiki.alpinelinux.org/wiki/Classic_install_or_sys_mode_on_Raspberry_Pi>
