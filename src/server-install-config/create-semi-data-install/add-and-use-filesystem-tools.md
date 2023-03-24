---
date: 2022-04-30
title: Add and use filesystem tools
tags: ["alpine","linux","self-host","sysadmin-devops"]
series: ["docs4web","alpine-linux-local-server"]
description: "You need to add the tools that will let you format/create one or more additional volumes/filesystems of your choice."
summary: "You need to add the tools that will let you format/create one or more additional volumes/filesystems of your choice."
---

## Overview

You need to add the tools that will let you format/create one or more additional volumes/filesystems of your choice.

## F2FS

A new flash file system for Linux; recommended for any flash (SD card, USB, etc)

* Install filesystem tools

  ```shell
  apk add f2fs-tools
  ```

* Create filesystem (sample session)

  ```shell
  mkfs.f2fs /dev/sda3
  ```

## Ext2/Ext4

A venerable Linux filesystem. Well supported (on non-UEFI x86/x86-64 systems one can boot from ext4 if one uses `extlinux` or `grub2` instead of `syslinux`)

* Install package

  ```shell
  apk add e2fsprogs
  ```

* Create filesystem (sample session)

  ```shell
  mkfs.ext4 -E lazy_itable_init=0,lazy_journal_init=0 /dev/sda3
  ```

## VFAT/FAT32/FAT16

The old standby from MS-DOS days and still used (as FAT32/ESP) for UEFI that is also used by many ARM bootloaders, including the one on the Raspberry Pi.

* Install package

  ```shell
  apk add dosfstools
  ```

* Create filesystem (sample session)

  ```shell
  mkfs.vfat -F 32 /dev/sda1
  ```

## LVM

For resizeable volumes, RAID, and more; is not a filesystem itself

```shell
apk add lvm2
```

## Btrfs

Can be used in place of LVM+ext4 or even RAID+LVM+ext4.

```shell
apk add btrfs-progs
```

## ZFS

Can be used in place of LVM+ext4 or even RAID+LVM+ext4.

```shell
apk add zfs
```

## mdadm

Traditional Linux software RAID.

```shell
apk add mdadm
```

## Useful links

<https://wiki.alpinelinux.org/wiki/Setting_up_a_software_RAID_array>
