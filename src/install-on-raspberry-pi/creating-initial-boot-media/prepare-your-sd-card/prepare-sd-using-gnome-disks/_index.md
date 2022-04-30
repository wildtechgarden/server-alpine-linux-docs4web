---
date: 2022-04-29
title: Prepare SD card using GNOME Disks
tags: ["alpine","configuration","docs","linux","sysadmin-devops","raspberry-pi","sbc"]
series: ["docs4web","alpine-linux-local-server"]
---

# Prepare SD card using GNOME Disks

## Overview

TBD

## Procedure

1. Start with an empty (unpartitioned, unformatted) SD card. If you disk is not empty, you will need to do a search on how to clean the disk and create an `msdos` disklabel (aka partition table).
   
   [![Gnome Disks showing an empty, unpartitioned SD card](01-gnome-disks-empty-sd-card.png)](01-gnome-disks-empty-sd-card.png)

2. Add boot partition
   [![Gnome Disks while adding a primary partition](02-gnome-disks-add-boot-partition.png)](02-gnome-disks-add-boot-partition.png)

3. Format as VFAT (part of partition-creation wizard)
   [![Gnome Disks add parition wizard format as vfat](03-gnome-disks-format-boot-as-vfat.png)](03-gnome-disks-format-boot-as-vfat.png)

4. Result is a partition formatted as FAT 16
   [![Gnome Disks showing SD card with FAT 16 boot partition](04-gnome-disks-sd-card-with-boot-partition.png)](04-gnome-disks-sd-card-with-boot-partition.png)

5. Make the partition bootable
   [![Gnome Disks setting partition as bootable](05-gnome-disks-make-partition-bootable.png)](05-gnome-disks-make-partition-bootable.png)

6. We want FAT 32 so use terminal to reformat as FAT 32
   [![Drop to terminal to reformat as FAT 32 because GNOME disks doesn't have that option](06-terminal-reformat-as-fat32.png)](06-terminal-reformat-as-fat32.png)

7. Resulting FAT 32 formatted boot partition
   [![Gnome Disks showing boot parition formatted as FAT 32](07-gnome-disks-sd-card-with-fat32-boot-partition.png)](07-gnome-disks-sd-card-with-fat32-boot-partition.png)

8. Mount the boot partition for next steps
   [![Gnome Disks showing boot partition mounted](08-gnome-disks-sd-card-mounted-boot-partition.png)](08-gnome-disks-sd-card-mounted-boot-partition.png)
