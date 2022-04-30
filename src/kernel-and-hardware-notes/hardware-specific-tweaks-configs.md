---
date: 2022-04-29
title: Hardware-specific tweaks and configuration
tags: ["alpine","docs","hardware","kernel","linux","sysadmin-devops"]
series: ["docs4web","alpine-linux-local-server"]
---

# Hardware-specific tweaks and configuration

Overview
--------

TBD

System with No RTC (real-time clock)
------------------------------------

Includes the Raspberry Pi family of SBC (single board computers).

1. Disable hwclock (if enabled)
   
   ```shell
   service hwclock stop
   rc-update hwclock disable boot default
   ```

2. Enable swclock
   
   ```shell
   rc-update swclock enable boot default
   service swclock start
   ```

Low entropy systems
-------------------

Includes headless Raspberry Pi systems.

1. Add and enable HAVEGED  package
   
   ```shell
   apk add haveged
   rc-update add haveged boot default
   service haveged start
   ```

Wireless
--------

TBD

Kernel commandline or device-tree / config
------------------------------------------

[Guides for setting kernel parameters](guides-for-setting-kernel-parameters.md)
