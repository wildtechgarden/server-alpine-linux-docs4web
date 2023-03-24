---
date: 2022-04-29
title: Prepare your SD card
tags: ["alpine","linux","sysadmin-devops","raspberry-pi"]
series: ["docs4web","alpine-linux-local-server"]
description: "Prepare the filesystem of the Alpine Linux bootstrap SD card for your Raspberry Pi"
summary: "Prepare the filesystem of the Alpine Linux bootstrap SD card for your Raspberry Pi"
---

## Partition the SD card

### Windows 10 Partitioning

#### Using built-in GUI 'Disk Management' feature

TBD

#### Using diskpart

TBD

#### Using PowerShell

TBD

### Linux (many distros) Partitioning

#### GUI

[Using Gnome 'Disks' applet](prepare-sd-using-gnome-disks/_index.md)

#### Using command line (CLI)

[Partitioning on the Linux command line](../../../linux-cli-partitioning/_index.md)

[Creating a filesystem on the Linux command line](../../../server-install-config/create-semi-data-install/add-and-use-filesystem-tools.md#vfatfat32fat16)

### Mac OS Partitioning

TBD

## Copy the tarball contents to 'boot' partition

### Tarball extract on Windows 10

You will need to install a program such a [7-zip](https://www.7-zip.org/)

TBD

### Tarball extract on Linux (many distros)

[Copy install tarball to boot partition using GUI file manager](copy-tarball-to-boot-under-gnome/_index.md)

#### Using CLI commands

Assuming you have mounted your new boot partition on `/mnt` you can (as root) do:

```shell
tar -C /mnt -xzf /path/to/install-tarball.tar.gz
```

### Tarball extract on Mac OS

TBD
