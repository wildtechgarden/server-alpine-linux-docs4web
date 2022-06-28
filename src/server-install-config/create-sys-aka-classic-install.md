---
date: 2022-06-27
title: "Create 'sys' aka 'classic' install"
tags: ["alpine","configuration","docs","hosting","linux","self-host","storage","sysadmin-devops","raspberry-pi","sbc"]
series: ["docs4web","alpine-linux-local-server"]
---

# Create encrypted LVM 'sys' aka 'classic' install

## Overview

## Use modified 'setup-alpine' procedure

### Notes

* Only tested on Alpine Linux 3.16.0. Earlier versions may not handle this scenario.
* If you use two disk devices instead of  \<disk-device> the script will create a RAID 1 array
* If you use more than two disk devices instead of \<disk-device> the script will create a RAID 5 array
* You can also adjust the size of the swap partition with `-s <SWAPSIZE>` in `DISKOPTS`
* I recommend either not creating an admin user when prompted (and creating one after the install) OR using a very simple password for the new user, and updating the password after the install. The reasoning is that with Alpine 3.16.0, which added the new user addition, there is an error in adduser logic such that if you do not correctly enter the password twice (password and confirmation) then you will end up stuck in an error loop you can't exit except by aborting the install, rebooting, and trying again. In addition, the new user's home directory does not survive the first reboot. (After firstboot, if you create a user on a system/classic install, this does not occur; the issue has to do with what directories are preserved by the install/diskless system).

### Commands

```shell
# Encrypted LVM
DISKOPTS="-eL -m sys <disk-device>" setup-alpine
```

where \<disk-device> is an entire disk (not a partition), such as `/dev/sda` (typical x86_64 system). With x86_64 systems be careful though, you want the hard disk(s) not the boot media (which maybe a `/dev/sdX` disk, including a chance of being `/dev/sda`).

**NB**: For the Raspbery Pi you must _omit_ \<disk-device> and enter `y` when prompted whether to use the boot media (`/boot/mmcblk0p1`) and to enter `y` again for the prompt on whether to erase an use the the entire disk (`mmcblk0`). This is because you will be erasing the boot media and replacing it with a 'classic' OS install. This does mean the process will be interactive at that point, because `setup-alpine` does not currently have a fully automated way to achieve the goal of replacing the boot install with the 'sys' mode install.
