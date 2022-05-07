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

* [Setup network required for installation of needed packages](setup-network-for-package-install.md)
* Install the partitioner and a tool to help identify the correct device to use

```shell
apk add parted lsblk
```

* List block devices to see the disks currently available

```shell
lsblk
```

* TBD

* A sample session
  
  ```shell
  parted /dev/sda
  ```

  mklabel gpt
  mkpart primary fat32 1 1G
  mkpart primary linux-swap 1G 3G
  mkpart primary f2fs 3G 13G
  mkpart primary f2fs 13G 15G
  toggle 1 esp
  quit

```
* List the resulting block devices

```shell
lsblk
```

## Using fdisk

Available on many distributions as part of the core install. Not suitable for setting up a UEFI install when using the fdisk version baked into the boot media in Alpine (it is a very limited version of fdisk).

TBD

## 

## Using sfdisk

Also requires adding a package, but can be automated more easily than parted or fdisk.

* [Setup network required for installation of needed packages](setup-network-for-package-install.md)
* TBD
