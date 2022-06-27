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

**Note** that with diskless, data, and our hybrid install, `lbu commit` only stores changes that are used after the 'boot' runlevel completes and cannot modify the 'boot' or 'sysinit' runlevels. While there are ways (if using a writable boot medium) to make modification in those early stages, doing so is out of scope for this documentation.

## Organize and configure storage on the system

We don't cover using encrypted storage here, yet. In the meantime, if you want to try adding it yourself, install the `dmcrypt` package and configure appropriately. There are some 'gotchas' with checking and mounting filesystems due not being able to modify the 'boot' or 'sysinit' runlevels that require using advanced features of OpenRC to manage the initscripts.

### Create a 'diskless' install as base and boot into it

#### For Raspberry Pi systems

If you followed [Installation on Raspberry Pi](../../install-on-raspberry-pi/_index.md) the diskless part is already the default, so skip to [add a config partition](#add-a-and39configand39-partition).

#### For x86_64 or x86 systems

##### Create the boot partition on the system's storage

* You need to add at least one package, which means doing some network setup. Then you can create the filesystem.
* [Setup network required for installation of needed packages](setup-network-for-package-install.md)
* Use fat32 or ext2/ext4 as boot partition if BIOS boot; for UEFI use FAT 32 and then mark as ESP (see [Linux command line partitioning](../../linux-cli-partitioning/_index.md)).
* [Add and use filesystem tools to create your choice of filesystem](add-and-use-filesystem-tools.md)
* We can't save the configuration yet, so these packages will disappear on reboot. That will not prevent the system from booting, as long as you avoid boot on LVM or boot on RAID.

##### Copy boot files to the boot partition

Sample session when `/dev/sdb` has been identified as the boot USB stick (or `/dev/sr0` for CD-ROM) and `/dev/sda` is your target disk formatted as discussed.

```shell
setup-bootable /dev/sdb1 /dev/sda1
```

##### Configure boot loader (extras)

See [hardware specific tweaks & configuration](../../kernel-and-hardware-notes/guides-for-setting-kernel-parameters.md).

##### Reboot

* You may need to update your system's configuration (e.g. BIOS setup) to boot from the new boot partition before Alpine will start up on the new system.

* It may also help to remove the installation media once the system has started to reset during reboot.

  ```shell
  reboot
  ```

The rest of this guide is now in sync regardless of whether you are starting with a Pi (or other ARM) install, or an x86_64/x86 system.

### Add a 'config' partition

#### Options

##### Using f2fs

* Useful if your media has limited write cycles even if much more than USB/SD flash (e.g. SSD, NVMe, etc)

* This is this author's recommended filesystem for the 'config' partition regardless of storage type for the Raspberry Pi (with x86_64 it is unfortunately not included in the stock initial boot disk — initramfs — and therefore we can't depend on it during boot).

* This filesystem has no 2 GB file size limit but it's still not a good sign if your overlays are getting that large (for 'semi-data' install)

* If you have < 8 GB of total available disk you may want to only have the boot partition, maybe a swap partition (non-flash drives only), and the 'config' partition

##### Using ext4

* Same notes as f2fs except that f2fs is the preferred choice on the Pi (ext4 is preferred on x86_64)

##### Using FAT 32

* Life is easy (but still not recommended to use) if one uses fat32 to store configs and APK cache as well (as a second partition).
* Since the configs shouldn't get too large, the largest chunk will be the the APK cache (so the 2GB max file size should not be an issue).
* Create `/media/name-of-partition` and add mount to `/etc/fstab`
* This option allows to skip network setup as it is 'baked' into boot system.

#### Create and enable 'config' partition

* You need to add at least one package, which means doing some network setup. Then you can create the filesystem.
* [Setup network required for installation of needed packages](setup-network-for-package-install.md)
* Add additional partitions. Like [creating boot partitions](../../linux-cli-partitioning/_index.md) except that we don't create a new partition table, we just add additional partitions.
* [Add and use filesystem tools to create your choice of filesystem](add-and-use-filesystem-tools.md)
* `mkdir /media/name-of-partition` and add mount to `/etc/fstab`
* **IMPORTANT**: `mount -a` and then `mount` to verify that the config partition is in fact mounted. If you don't mount the partition, `setup-alpine` won't 'see' it as available.

### Possibly add a swap partition

* On appropriate media (e.g. not SD card or flash; better is to use an external drive if one must use swap and the base OS is on SD or flash)

* Create a partition to hold the swap

* `mkswap /dev/device-with-swap`

* add to `fstab`

   * For example, if `/dev/device-with-swap` was `/dev/mmcblk0p3` we would add:

     ```fstab
     /dev/mmcblk0p3 swap swap swap 0 0
     ```

   * Execute `swapon -a`

### All other partitions

#### Options

##### For large non-flash storage use LVM and ext4 or on x86_64 always

* This makes resizing partitions at least possible, with a filesystem (ext4) that is well-supported by Alpine
* Instead of LVM+ext4 one could use btrfs or zfs, or LVM+some other filesystem, but this is out of scope and less supported.
* This discussion assumes a single drive; like the comments on using btrfs or zfs using RAID and/or other multiple drive setups is out of scope and needs advanced Linux knowledge.
* Once you create the volume, create the filesystem,
* Add to fstab

##### For small storage (<= 8 GB)

Don't use additional partitions just use boot, config, and maybe swap (non-flash).

##### For large flash storage (including SD cards), use f2fs directly

* We need to minimize writes, and to use an appropriate filesystem. Also, no LVM.
* Since (at least for non-UEFI) the boot structure requires MS-DOS partition table type (aka disk label), use logical partitions so you can have the partitions you want.
* Prefer fewer and larger partitions since resizing would be difficult in this scenario.
* Also one may want to keep logging on `tmpfs` unless one requires persistence across reboots (and then this author recommends using non-flash external storage or sending to logs to another system with non-flash disks).
* Trying to do resizing here will not make you happy. Also we will be mounting specific (low-write) partitions (using bind mount), so would need a lot of small partitions to get the same effect, which is hard to manage.

#### Mount (or bind mount) /home

##### Small storage or only flash storage

That means you have configured one 'boot' partition an one 'config' on the storage, so in order to make more than what you 'commit' via LBU persistent you need to point the directory (or directories) each to a corresponding directory on the 'config' partition.

Example with 'config' mounted on `/media/mmcblk0p2`

1. Make sure `/home` exists and is empty

2. `mkdir -p /media/mmcblk0p2/data/home`

3. Edit `/etc/fstab` to add

   ```shell
   /media/mmcblk0p2/data/home /home none bind,rw 0 0
   ```

4. `mount /home` to activate the bind mount

5. Issue `df -h`; it should list the new mount

6. Issue `mount | grep /home`; it should also list the new mount

7. `/home` is now ready for storing you user home directories.

##### Large non-flash storage

In this case you should create a volume, add to `/etc/fstab`, and `mount` as you would for any command line Linux system.

#### Bind mount some /var/lib sub-directories (base install)

You may need to repeat this procedure for directories for some packages you install.

It is only useful to do this for packages that need to preserve data for use across reboot and which don't need the preserved data until after the 'sysinit' and 'boot' phases have completed, since the 'config' partition will not be available until then.

##### Network time client 'drift'

Assuming you have used the default NTP client (`chronyd`):

The directory to preserve is `/var/lib/chrony`. One could create `/media/mmcblk0p2/data/var/lib/chrony` and have an `fstab` with

```shell
/media/mmcblk0p2/data/var/lib/chrony /var/lib/chrony none bind,rw 0 0
```

##### Randomness for seeding next boot

This is needed during boot so doesn't make sense unless you are modifying the initramfs.

The directory to preserve is `/var/lib/seedrng`. One could create `/media/mmcblk0p2/data/var/lib/seedrng` and have an `fstab` with

```shell
/media/mmcblk0p2/data/var/lib/seedrng /var/lib/seedrng none bind,rw 0 0
```

##### DHCP client lease and other preferably persistent data

This is needed during boot so doesn't make sense unless you are modifying the initramfs.

The directory to preserve is `/var/lib/udhcpd`. One could create `/media/mmcblk0p2/data/var/lib/udhcpd` and have an `fstab` with

```shell
/media/mmcblk0p2/data/var/lib/uhdcpd /var/lib/udhcpd none bind,rw 0 0
```

#### Mount /var/log on non-flash storage, if available

Keeping `/var/log` persistent is sometimes required, but logging usually involves much writing to storage and quickly uses flash write cycles. In addition having `/var/log` as a separate partition limits the damage that can occur when some process start spamming the logs. If the logs are in their own partition, it avoids all of `/var` (or the entire filesystem if you only have one big partition) becoming full and bringing the system to its knees.

If you do not have non-flash storage available you should prefer sending the logs to another system (remote syslog) to using even a limited log partition.

If you want a separate `/var/log`, you should create a volume on non-flash storage, add to `/etc/fstab`, and `mount` as you would for any command line Linux system.

However, before doing `mount` you probably want to move the current `/var/log` contents to the new location (by temporarily mounting the new location on `/mnt`, halting any logging processes, doing `mv /var/log/* /mnt/`, and `umount /mnt`).

## Remove partitioning tools

In the interests of saving space on the system during normal use and reducing chances of human error, remove `parted` if you used that for partitioning.

```shell
apk del parted
```
