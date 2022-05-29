---
date: 2022-04-29
title: Hardware-specific tweaks and configuration
tags: ["alpine","docs","hardware","kernel","linux","sysadmin-devops"]
series: ["docs4web","alpine-linux-local-server"]
---

# Hardware-specific tweaks and configuration

## Systems with No RTC (real-time clock)

Includes the Raspberry Pi family of SBC (single board computers).

1. Disable hwclock (if enabled; on the Raspberry Pi it has already been disabled).

   ``` shell
   service hwclock stop
   rc-update hwclock disable boot
   ```

2. Enable swclock (only useful if `/sbin/openrc-run` is preserved across boots. For a system mode (classic) install this helps. For a diskless, data, or our hybrid install, it isn't. Also note that for the Raspberry Pi it comes pre-enabled.

   ```shell
   rc-update swclock enable boot
   service swclock start
   ```

## Low entropy systems

Includes headless Raspberry Pi systems.

1. Add and enable HAVEGED  package

   ```shell
   apk add haveged
   rc-update add haveged boot default
   service haveged start
   ```

## Wireless

TBD

## Kernel commandline or device-tree / config

[Guides for setting kernel parameters](guides-for-setting-kernel-parameters.md)
