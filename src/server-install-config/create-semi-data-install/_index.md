---
date: 2022-04-28
title: Create semi-data/semi-diskless install
tags: ["alpine","configuration","docs","hosting","linux","self-host","storage","sysadmin-devops","raspberry-pi","sbc"]
series: ["docs4web","alpine-linux-local-server"]
---

# Create semi-data/semi-diskless install

## Overview

Like diskless except that `home`, parts of `/var`, and others are mounted for persistence. Like data install except that only pars of `/var` are made persistent.

Organize and Configure Storage
------------------------------

We don't cover using encrypted storage; that gets complicated fast and is out of scope.

### Create a 'diskless' install as base

For [Installation on Raspberry Pi](../../install-on-raspberry-pi/_index.md) the diskless part is already the default

#### For non-Raspberry Pi systems

* Use fat32 as boot partition if BIOS boot; for UEFI use FAT 32 and mark as ESP (UEFI out of scope for now)
* Copy boot files
* Configure boot loader

### Add a 'config' partition

#### Options

##### Using f2fs

* Useful if your media has limited write cycles even if much more than USB/SD flash (e.g. SSD, NVMe, etc)

* This author's recommended filesystem for the 'config' partition regardless of storage type.

* no 2 GB file size limit but it's still not a good sign if your overlays are getting that large (for 'semi-data' install)

* If you have < 8 GB of total available disk you may want to only have the boot partition, maybe a swap partition (non-flash drives only), and the 'config' partition

##### Using ext4

* Same notes as f2fs except that f2fs is the preferred choice

##### Using FAT 32

* Life is easy (but still not recommended to use) if one uses fat32 to store configs and APK cache as well (as a second partition).
* Since the configs shouldn't get too large, the largest chunk will be the the APK cache (so the 2GB max file size should not be an issue).
* Create `/media/name-of-partition` and add mount to `/etc/fstab`
* This option allows to skip network setup as it is 'baked' into boot system.

#### Create and enable 'config' partition

You need to add at least one package, which means doing some network setup. Then you can create the filesystem.

* Create `/media/name-of-partition` and add mount to `/etc/fstab`
* **IMPORTANT**: `mount -a` and then `mount` to verify that the config partition is in fact mounted. If you don't mount the partition, `setup-alpine` won't 'see' it as available.

[Setup network required for installation of needed packages](setup-network-for-package-install.md)
[Add and use filesystem tools to create your choice of filesystem](add-and-use-filesystem-tools.md)

### Add a swap partition

* On appropriate media (e.g. not SD card or flash; better is to use an external drive if one must use swap and the base OS is on SD or flash)
* Create a partition to hold the swap
* mkswap
* add to fstab

### All other partitions

#### For large non-flash storage use LVM and ext4

* This makes resizing partitions at least possible, with a filesystem (ext4) that is well-supported by Alpine
* Instead of LVM+ext4 one could use btrfs or zfs, or LVM+some other filesystem, but this is out of scope and less supported by the distro
* This discussion assumes a single drive; like using btrfs or zfs using RAID and/or other multiple drive setups is out of scope and needs advanced Linux knowledge.
* Once you create the volume, create the filesystem
* Add to fstab

#### For small storage (<= 8 GB)

Don't use additional partitions just use boot, config, and maybe swap (non-flash)

#### For large flash storage (including SD cards), use f2fs directly

* We need to minimize writes, and to use an appropriate filesystem. Also, no LVM.
* Since (at least for non-UEFI) the boot structure requires MS-DOS partition table type (aka disk label), use logical partitions so you can have the partitions you want.
* Prefer fewer and larger partitions since resizing would be difficult in this scenario.
* Also may want to keep logging on ``tmpfs`` unless one requires persistence across reboots (and then this author recommends using non-flash external storage or sending to logs to another system with non-flash disks).
* Trying to do resizing here will not make you happy. Also we will be bind mounting specific (low-write) partitions, so would need a lot of small partitions, which is hard to manage. KISS.

Remove partitioning tools
-------------------------

* In the interests of saving space on the system during normal use and reducing chances of human error, remove ``parted`` if you used that for partitioning
