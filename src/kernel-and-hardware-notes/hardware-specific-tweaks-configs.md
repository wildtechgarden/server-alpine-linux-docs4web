---
date: 2022-04-29
title: Hardware-specific tweaks and configuration
tags: ["alpine","linux","sysadmin-devops","raspberry-pi"]
series: ["docs4web","alpine-linux-local-server"]
description: "Tweaks to Alpine Linux for specific hardware including packages and kernel parameters"
summary: "Tweaks to Alpine Linux for specific hardware including packages and kernel parameters"
---

## Systems with No RTC (real-time clock)

Includes the Raspberry Pi family of SBC (single board computers).

1. Disable hwclock (if enabled; on the Raspberry Pi it has already been disabled).

   ```shell
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

1. Add and enable RNG tools package

    * The Raspberry Pi has a hardware RNG
    * rng-tools includes the 'jitter' entropy source which is an improvement on 'haveged' so we recommend using `rng-tools` rather than the `haveged` package. (Thank you to Dermot Bradley for pointing this out).

   ```shell
   apk add rng-tools
   rc-update add rngd boot default
   service rngd start
   ```

## Wireless

TBD

## Kernel commandline or device-tree / config

[Guides for setting kernel parameters](guides-for-setting-kernel-parameters.md)
