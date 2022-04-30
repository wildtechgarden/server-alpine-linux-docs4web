---
date: 2022-04-28
title: Server install & configure
tags: ["alpine","configuration","docs","hosting","linux","self-host","sysadmin-devops","raspberry-pi","sbc"]
series: ["docs4web","alpine-linux-local-server"]
---

# Server install & configure

## Overview

This set of guides and recommendations is aimed at the use of Alpine as your local servers on physical hardware where you have access to the console on boot. Notes for differences with headless installations (but still local) are included inline.

Cloud / production deployments remain to be added (ideally in a mature production environment one would never access an interactive shell on the server, so no SSH, no console enhancements, and no online documentation like man pages for shell users). Cloud deployment would also tend to not use the 'diskless / data' style of deployment outlined here, since one should be doing a more advanced division of OS from persistent data in that type of scenario.

Also not documented here is 'automated' installation and configuration, although likely I will be adding that based on these pages in another set of guides.

Guides
------

1. [Create semi-data/semi-diskless install](create-semi-data-install/_index.md)
2. [Use modified setup-alpine procedure](use-modified-setup-alpine-procedure.md)
3. [Add essential packages](add-essential-packages.md)
4. [Commit LBU](commit-lbu.md)
5. [Reboot](reboot.md) 
6. [Kernel and hardware notes - hardware specific tweaks & configuration](../kernel-and-hardware-notes/hardware-specific-tweaks-configs.md)

## See also

[Recommended tweaks and configuration](../recommended-tweaks-and-configs/_index.md)

Troubleshooting
---------------

* [First boot troubleshooting](firstboot-troubleshooting.md)
