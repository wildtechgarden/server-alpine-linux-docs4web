---
date: 2022-04-29
title: Guides for setting kernel parameters
tags: ["alpine","kernel","linux","sysadmin-devops"]
series: ["docs4web","alpine-linux-local-server"]
description: "Information on setting kernel parameters for Alpine Linux"
summary: "Information on setting kernel parameters for Alpine Linux"
---

## Overview

These vary with architecture and specific device

## Linux kernel guide to its parameters

<https://www.kernel.org/doc/html/latest/admin-guide/kernel-parameters.html>

## A suggested tweak

Adding `consoleblank=300` can be a nice addition to the kernel commandline. It blanks a text console if left idle for over 300 seconds (5 minutes). In same cases that will allow a monitor to do some power saving (although it is not display 'sleep' mode).

### Modifying files on the boot partition

If your boot partition is mounted on `/media/mmcblk0p1`, you need to make `/media/mmcblk0p1` read-write before you can make changes. To do so execute:

```shell
mount -o remount,rw /media/mmcblk0p1
```

change what you need, then return to read-only status

```shell
mount -o remount,ro /media/mmcblk0p1
```

**Hint**: Typical x86-64 systems will likely use `/media/sda1` rather than `/media/mmcblk0`. You will need to verify the name of the storage device and adjust these instructions accordingly.

**NOTE**: It is recommended that you do **not** make this partition read-write under normal conditions. This avoids accidental writes which could render your system unbootable.

## Systems using Syslinux for bootloader

**WARNING:** Changing the kernel commandline or boot configuration can render your system unbootable, depending on the parameters you change.

Edit `syslinux.cfg` in the boot partition. For example, `/media/sda1/boot/syslinux/syslinux.cfg`.

The default x86-64 commandline in `syslinux.cfg`:

```shell
APPEND modules=loop,squashfs,sd-mod,usb-storage quiet
```

## Systems using GRUB for bootloader

**WARNING:** Changing the kernel commandline or boot configuration can render your system unbootable, depending on the parameters you change.

Edit `grub.cfg` in the boot partition. For example, `/media/sda1/boot/grub/grub.cfg`

The default x86-64 commandline in `grub.cfg`:

```shell
linux    /boot/vmlinuz-lts modules=loop,squashfs,sd-mod,usb-storage quiet
```

## Systems using U-boot

TBD

## Raspberry Pi

### Kernel parameter setting (boot time)

**WARNING:** Changing the kernel commandline can render your system unbootable, depending on the parameters you change.

`/media/mmcblk0p1/commandline.txt` is passed verbatim to the kernel at the end of the kernel commandline. Edit to suit your needs.

### Device-tree (config.txt/usercfg.txt)

> See [GrayJack's very complete and documented config.txt file for raspberry pi on GitHub (Gist)](https://gist.github.com/GrayJack/2b27cdaf9a6432da7c5d8017a1b99030) for information.

`/media/mmcblk0p1/usercfg.txt`: The preferred location for setting certain hardware configuration options.

`/media/mmcblk0p1/config.txt` : Is *replaced* on kernel updates so it is recommended that you do not use this location for your settings. Instead use *`usercfg.txt`*. Unfortunately, some parameters like `gpu_mem=32` will not be honoured in `usercfg.txt` and therefore you must edit `config.txt` and remember to update on kernel update. (see [Raspberry Pi firmware GitHub issue #1332](https://github.com/raspberrypi/firmware/issues/1332))
