---
date: 2022-04-28
title: Create semi-data/semi-diskless install
tags: ["alpine","configuration","docs","hosting","linux","self-host","storage","sysadmin-devops","raspberry-pi","sbc"]
series: ["docs4web","alpine-linux-local-server"]
---

# Create semi-data/semi-diskless install

## Overview

This guide presumes you are booted into a fresh install media (no stored configuration). It further presumes that neither the [pure diskless configuration from the Alpine wiki](https://wiki.alpinelinux.org/wiki/Installation#Diskless_Mode), the [data configuration from the Alpine wiki](https://wiki.alpinelinux.org/wiki/Installation#Data_Disk_Mode), nor the [system disk (classic) configuration from the Alpine wiki](https://wiki.alpinelinux.org/wiki/Installation#System_Disk_Mode) suits your situation.

This configuration is like diskless mode except that `home`, parts of `/var`, and others are mounted for persistence. It is also like data install except that only _parts_ of `/var` are made persistent.

Organize and configure storage on the system
------------------------------

We don't cover using encrypted storage; explaining the details is out of scope.

### Create a 'diskless' install as base and boot into it

#### For Raspberry Pi systems

If you followed [Installation on Raspberry Pi](../../install-on-raspberry-pi/_index.md) the diskless part is already the default, so skip to [add a config partition](#ad-a-and39configand39-partition).

#### For non-Raspberry Pi systems

##### Create the boot partition on the system's storage

* You need to add at least one package, which means doing some network setup. Then you can create the filesystem.
* Use fat32 as boot partition if BIOS boot; for UEFI use FAT 32 and then mark as ESP (see [Linux command line partitioning](../../linux-cli-partitioning/_index.md)).
* [Setup network required for installation of needed packages](setup-network-for-package-install.md)
* [Add and use filesystem tools to create your choice of filesystem](add-and-use-filesystem-tools.md)

##### Copy boot files to the boot partition

TBD

##### Configure boot loader

TBD

##### Reboot

```shell
reboot
```

* You may need to update your system's configuration to boot from the new boot partition before Alpine will start up on the new system.
* It may also help to remove the installation media once the system has started to reset during reboot.

Now you system is operating like the initial boot of a Raspberry Pi.

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

* You need to add at least one package, which means doing some network setup. Then you can create the filesystem.
* [Setup network required for installation of needed packages](setup-network-for-package-install.md)
* [Add and use filesystem tools to create your choice of filesystem](add-and-use-filesystem-tools.md)
* `mkdir /media/name-of-partition` and add mount to `/etc/fstab`
* **IMPORTANT**: `mount -a` and then `mount` to verify that the config partition is in fact mounted. If you don't mount the partition, `setup-alpine` won't 'see' it as available.

### Possibly add a swap partition

* On appropriate media (e.g. not SD card or flash; better is to use an external drive if one must use swap and the base OS is on SD or flash)
* Create a partition to hold the swap
* mkswap
* add to fstab

### All other partitions

#### For large non-flash storage use LVM and ext4

* This makes resizing partitions at least possible, with a filesystem (ext4) that is well-supported by Alpine
* Instead of LVM+ext4 one could use btrfs or zfs, or LVM+some other filesystem, but this is out of scope and less supported.
* This discussion assumes a single drive; like the comments on using btrfs or zfs using RAID and/or other multiple drive setups is out of scope and needs advanced Linux knowledge.
* Once you create the volume, create the filesystem,
* Add to fstab

#### For small storage (<= 8 GB)

Don't use additional partitions just use boot, config, and maybe swap (non-flash)

#### For large flash storage (including SD cards), use f2fs directly

* We need to minimize writes, and to use an appropriate filesystem. Also, no LVM.
* Since (at least for non-UEFI) the boot structure requires MS-DOS partition table type (aka disk label), use logical partitions so you can have the partitions you want.
* Prefer fewer and larger partitions since resizing would be difficult in this scenario.
* Also may want to keep logging on ``tmpfs`` unless one requires persistence across reboots (and then this author recommends using non-flash external storage or sending to logs to another system with non-flash disks).
* Trying to do resizing here will not make you happy. Also we will be bind mounting specific (low-write) partitions, so would need a lot of small partitions, which is hard to manage. Keep it simple.

Remove partitioning tools
-------------------------

* In the interests of saving space on the system during normal use and reducing chances of human error, remove ``parted`` if you used that for partitioning
