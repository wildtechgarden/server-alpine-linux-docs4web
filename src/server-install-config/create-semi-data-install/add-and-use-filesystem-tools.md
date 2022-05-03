---
date: 2022-04-30
title: Add and use filesystem tools
tags: ["alpine","configuration","docs","filesystem", "hosting","linux","self-host","storage","sysadmin-devops","raspberry-pi","sbc"]
series: ["docs4web","alpine-linux-local-server"]
---

# Add and use filesystem tools

## Overview

You need to add the tools that will let you format/create one or more additional volumes/filesystems of your choice.

## F2FS

A new flash file system for Linux; recommended for any flash (SD card, USB, etc)

```shell
apk add f2fs-tools
```

## Ext2/Ext4

A venerable Linux filesystem. Well supported (on non-UEFI x86/x86-64 systems one can boot from ext4 if one uses `extlinux` or `grub2` instead of `syslinux`)

```shell
apk add e2fsprogs
```

## VFAT/FAT32/FAT16

The old standby from MS-DOS days and still used (as FAT32/ESP) for UEFI that is also used by many ARM bootloaders, including the one on the Raspberry Pi.

```shell
apk add dosfstools
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
