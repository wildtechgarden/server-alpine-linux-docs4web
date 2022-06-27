---
date: 2022-06-27
title: Choose installation type
tags: ["alpine","configuration","docs","hosting","linux","self-host","storage","sysadmin-devops","raspberry-pi","sbc"]
series: ["docs4web","alpine-linux-local-server"]
---

# Choose installation type

## A table of installation types

| Type of install                                                                                                | Description / properties                                                                                                                                                                                                                                                                                                   |
| -------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Pure diskless, from the Alpine wiki](https://wiki.alpinelinux.org/wiki/Installation#Diskless_Mode)            | Core OS is the same on every boot and data is lost on every boot, except for what is stored in a 'overlay' file on persistent storage (if any).                                                                                                                                                                            |
| [Data, fom the Alpine wiki](https://wiki.alpinelinux.org/wiki/Installation#Data_Disk_Mode)                     | Core OS is the same on every boot, however data is preserved across boots, and many OS changes can be preserved via an 'overlay' files. The data and 'overlay' are stored on persistent storage.                                                                                                                           |
| [System disk (classic), from the Alpine wiki](https://wiki.alpinelinux.org/wiki/Installation#System_Disk_Mode) | Fully persistent OS and data. A traditional (non-OStree) Linux distribution install.  None-encrypted by default. Except on Raspberry Pi, the easiest type of install in terms of avoiding 'gotchas' (least surprises). It is also the documented method in the [main Alpine documentation](https://docs.alpinelinux.org/). |
| [Semi-diskless/semi-data, described in this document collection](cretate-semi-data-install/_index.md)          | Core OS is the same on every boot, some data is preserved across boots, and many OS changes can be preserved via an 'overlay' file. The preserved data and 'overlay' are stored on persistent storage.                                                                                                                     |
| [Custom system disk (classic), described in this document collection](create-sys-aka-class-install/_index.md)  | Fully persistent OS and data. A traditional (non-OStree) Linux distribution install. This documentation includes setting of full disk encryption, enabling LVM, and (if applicable) RAID. We include documentation for doing this on a Raspberry Pi in addition to x86_64 (aka amd64) hardware.                            |

## Why you might pick a diskless/data style installation

* Runs from RAM, and is therefore very fast.
* Easy to revert the system in case of a bad configuration (until you commit the configuration); just reboot.
* If you keep previous versions of you configuration by configuring 'backups' in `lbu.conf` (really is keeping copies of previous configurations when committing a new version), then you can revert to a previous configuration by renaming the backup copy to the active copy name.

## Why you might not pick a diskless/data style installation

* Runs from RAM, which means there is less RAM available for the actual system.
* If you don't commit configuration changes and do a reboot, those changes are lost.
* For applications like 'libvirt' that automatically update their configuration based on CLI or GUI tools, you may not realize you have configuration you need to commit and may lose important configuration on reboot.
* For a semi-diskless/semi-data installation you need to know what needs to be preserved and add configuration to preserve that data.
* It is difficult to modify the configuration of the core OS, since it is in an initramfs instead of on an OS partition of a hard drive.

## Advantages of configurations described in this collection

* For the semi-diskless/semi-data installation you get the benefits of both diskless and data installs.
  * You also get a more complete and consistent guide than the wiki (although eventual goal is to update the wiki with the info, so this is a temporary benefit to this collection).
* For the custom system disk installation, you get a more complete / full featured installation in one set of guides instead of piecing together various documents (this is also a temporary benefit).
