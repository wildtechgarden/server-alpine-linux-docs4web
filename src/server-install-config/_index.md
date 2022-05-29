---
date: 2022-04-28
title: Server install & configure
tags: ["alpine","configuration","docs","hosting","linux","self-host","sysadmin-devops","raspberry-pi","sbc"]
series: ["docs4web","alpine-linux-local-server"]
---

# Server install & configure

## Overview

This set of guides and recommendations is aimed at the use of Alpine as your local servers on physical hardware where you have access to the console on boot.

Headless and cloud / production deployments remain to be added (ideally in a mature production environment one would never access an interactive shell on the server, so no SSH, no console enhancements, and no online documentation like man pages for shell users).

Also not documented here is fully 'automated' installation and configuration; that likely will be added based on these pages, but in another set of guides.

Finally, these guides would also work for systems in which one uses a flash device for the OS and OS data (e.g. a system running from a USB flash drive).

## Guides

1. [Obtain and verify the install media](../verify-downloaded-install-media/_index.md)
2. [Write the install image to bootable storage for x86_64/x86 (Alpine Linux wiki)](https://wiki.alpinelinux.org/wiki/Installation#Flashing_.28direct_data_writing.29_the_installation_image-file_onto_a_device_or_media) or [write the install tarball to your boot disk (e.g. SD card) for the Raspberry Pi](../install-on-raspberry-pi/creating-initial-boot-media/_index.md)
3. [Boot from the install media (Alpine Linux wiki)](https://wiki.alpinelinux.org/wiki/Installation#Booting_from_external_devices)
4. [Create a semi-data/semi-diskless install](create-semi-data-install/_index.md)
5. [Use modified setup-alpine procedure](use-modified-setup-alpine-procedure.md)
6. [Commit LBU](commit-lbu.md)
7. [Reboot](reboot.md)
8. [Kernel and hardware notes - hardware specific tweaks & configuration](../kernel-and-hardware-notes/hardware-specific-tweaks-configs.md)

## See also

[Important post install configuration](../important-post-install-configuration/_index.md)

[Recommended tweaks and configuration](../recommended-tweaks-and-configs/_index.md)

## Troubleshooting

* [First boot troubleshooting](firstboot-troubleshooting.md)
