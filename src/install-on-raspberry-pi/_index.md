---
date: 2022-04-29
title: Use Alpine Linux on Raspberry Pi as a server
tags: ["alpine","configuration","docs","hosting","linux","self-host","sysadmin-devops","raspberry-pi","sbc"]
series: ["docs4web","alpine-linux-local-server"]
---

# Use Alpine Linux on Raspberry Pi as a server

Motivation
----------

There are some less than stellar guides on the Alpine wiki

<https://wiki.alpinelinux.org/wiki/Raspberry_Pi>
<https://wiki.alpinelinux.org/wiki/Classic_install_or_sys_mode_on_Raspberry_Pi>

So here is an attempt at something better for a semi-diskless / semi-data install.

Special Notes
-------------

**NOTE:** For boot to succeed `/media/mmcblk0p1/usercfg.txt` must exist. See [Raspberry Pi kernel device-tree settings](kernel-and-hardware-notes/guides-for-setting-kernel-parameters.md) for information on what you can set in that file. A blank file is sufficient to allow booting, however.

Guides
------

[Creating initial boot media](creating-initial-boot-media/_index.md)
[Server install and configure](./ServerInstallConfig.md)

[Hardware-specific tweaks and configuration](../kernel-and-hardware-notes/hardware-specific-tweaks-configs.md)
