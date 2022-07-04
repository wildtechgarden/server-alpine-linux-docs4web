---
date: 2022-04-28
title: Server install & configure
tags: ["alpine","configuration","docs","hosting","linux","self-host","sysadmin-devops","raspberry-pi","sbc"]
series: ["docs4web","alpine-linux-local-server"]
---

# Server install & configure

## Overview

This set of guides and recommendations is aimed at the use of Alpine as your local servers on physical hardware where you have access to the console on boot.

Headless and cloud deployments remain to be added (cloud deployment work is in progress based on [Packer](https://packer.io), [Terraform](https://terraform.io), and [Vault](https://vaultproject.io) at the time of this writing [June 27, 2022]).

Also not documented here is fully 'automated' bare metal installation and configuration; that likely will be added based on these pages, but in another set of guides.

Finally, the semi-data/semi-diskless guides would also work for systems in which one uses a flash device for the OS and OS data (e.g. a system running from a USB flash drive).

## Guides

1. [Obtain and verify the install media](../verify-downloaded-install-media/_index.md)
2. [Write the install image to bootable storage for x86_64/x86 (Alpine Linux wiki)](https://wiki.alpinelinux.org/wiki/Installation#Flashing_.28direct_data_writing.29_the_installation_image-file_onto_a_device_or_media) or [write the install tarball to your boot disk (e.g. SD card) for the Raspberry Pi](../install-on-raspberry-pi/creating-initial-boot-media/_index.md)
3. [Boot from the install media (Alpine Linux wiki)](https://wiki.alpinelinux.org/wiki/Installation#Booting_from_external_devices)
4. [Choose install type](choose-install-type.md)
    1. [Create a semi-data/semi-diskless install](create-semi-data-install/_index.md)
        1. [Use modified setup-alpine procedure](use-modified-setup-alpine-procedure.md)
        2. [Commit LBU](commit-lbu.md)
    2. [Create an encrypted LVM 'sys' aka 'classic' install](create-sys-aka-classic-install.md)
5. [Reboot](reboot.md)
6. [Kernel and hardware notes - hardware specific tweaks & configuration](../kernel-and-hardware-notes/hardware-specific-tweaks-configs.md)

## See also

[Important post install configuration](../important-post-install-configuration/_index.md)

[Recommended tweaks and configuration](../recommended-tweaks-and-configs/_index.md)

['Create Alpine Disk Image' script by Dermot Bradley](https://github.com/dermotbradley/create-alpine-disk-image)

## Troubleshooting

* [First boot troubleshooting](firstboot-troubleshooting.md)
