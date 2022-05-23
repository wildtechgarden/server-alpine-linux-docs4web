---
date: 2022-05-01
title: Partitioning on the Linux command line
tags: ["alpine","configuration","docs","linux","sysadmin-devops"]
series: ["docs4web","alpine-linux-local-server"]
---

# Partitioning on the Linux command line

[Partitioning information in the official Alpine Linux User's Handbook](https://docs.alpinelinux.org/user-handbook/0.1a/Installing/manual.html#_partitioning_your_disk)

* For this guide we only consider two types of install: BIOS to 'msdos'-type partition table (disklabel) and UEFI to gpt partition table.
* While other options are possible, we are trying to avoid too many options. Many options is not only confusing but it is a lot more to document and keep up to date.

## Using parted

Easiest of the command line options, but requires adding a package on Alpine and others (some distros include parted by default, others do not).

* [Setup network required for installation of needed packages](../server-install-config/create-semi-data-install/setup-network-for-package-install.md)

* Install the partitioner and a tool to help identify the correct device to use
  
  ```shell
  apk add parted lsblk
  ```

* List block devices to see the disks currently available
  
  ```shell
  parted -l
  ```
  
  Would show something like:
  
  ```shell
  Model: ATA CT1000BX100SSD1 (scsi)
  Disk /dev/sda: 1000GB
  Sector size (logical/physical): 512B/512B
  Partition Table: msdos
  Disk Flags: 
  
  Number  Start  End  Size  Type  File system  Flags
  
  Model: CHIPSBNK v3.3.9.6 (scsi)
  Disk /dev/sdb: 2096MB
  Sector size (logical/physical): 512B/512B
  Partition Table: msdos
  Disk Flags: 
  
  Number  Start  End     Size    Type     File system  Flags
   2      154kB  1628kB  1475kB  primary               boot, esp
  ```

* Alternatively, using `lsblk`
  
  ```shell
  lsblk -o NAME,KNAME,PATH,FSTYPE,FSAVAIL,FSROOTS,LABEL
  ```
  
  Would show something like:
  
  ```plain
  NAME   KNAME PATH       FSTYPE   FSAVAIL FSROOTS LABEL
  loop0  loop0 /dev/loop0 squashfs       0 /       
  sda    sda   /dev/sda
  sdb    sdb   /dev/sdb   iso9660        0 /       alpine-std 3.15.4 x86_64
  └─sdb2 sdb2  /dev/sdb2  vfat                     
  sr0    sr0   /dev/sr0 
  ```

* The iso9660 is the CD image we 'burned' to usb in this case, so `/dev/sdb` is the install media. That means `/dev/sda` is the internal hard drive to which we wish to install. If we had boot from an actual CD-ROM we would see the iso9660 on `/dev/sr0` and there would be little chance of confusion with the hard drive.

* This leads to a parted session, on x86_64, such as
  
  ```shell
  parted /dev/sda
  mkpart primary fat32 1 1G
  toggle 1 esp
  quit
  ```

* On Raspberry Pi we must do this stage on another system, as discussed in the articles on the topic.

* List the resulting block devices
  
  ```shell
  lsblk -o NAME,KNAME,PATH,FSTYPE,FSAVAIL,FSROOTS,LABEL
  ```
  
  Giving something like
  
  ```plain
    NAME   KNAME PATH       FSTYPE   FSAVAIL FSROOTS LABEL
  loop0  loop0 /dev/loop0 squashfs       0 /       
  sda    sda   /dev/sda                            
  └─sda1 sda1  /dev/sda1  vfat                     
  sdb    sdb   /dev/sdb   iso9660        0 /       alpine-std 3.15.4 x86_64
  └─sdb2 sdb2  /dev/sdb2  vfat                     
  sr0    sr0   /dev/sr0 
  ```

## Using fdisk

Available on many distributions as part of the core install. Not suitable for setting up a UEFI install when using the fdisk version baked into the boot media in Alpine (it is a very limited version of fdisk).

TBD

## Using sfdisk

Also requires adding a package, but can be automated more easily than parted or fdisk.

* [Setup network required for installation of needed packages](../server-install-config/create-semi-data-install/setup-network-for-package-install.md)
* TBD
