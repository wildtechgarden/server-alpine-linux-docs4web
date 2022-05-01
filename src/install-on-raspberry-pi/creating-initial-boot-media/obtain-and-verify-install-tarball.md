---
date: 2022-04-29
title: Obtain and verify install tarball
tags: ["alpine","configuration","docs","linux","security","sysadmin-devops","raspberry-pi","sbc"]
series: ["docs4web","alpine-linux-local-server"]
---

# Obtain and verify install tarball

Obtain the official Alpine Linux image
--------------------------------------

### Choose tarball to download based on the model of Pi you have

Partial table of model of Raspberry Pi to Linux kernel max architecture available (where aarch64 > armv7 > armhf). armhf should be a 'safe' choice for all models, but aarch64 is preferred when possible, then armv7, then armhf.

| Model       | Arch       |
|:----------- |:---------- |
| Pi A        | armhf      |
| Pi B        | armhf      |
| Pi 2 A      | armhf      |
| Pi B+       | armhf      |
| Pi Zero     | armhf      |
| Pi Zero W   | armhf      |
| Pi 2 B      | armv7      |
| Pi Zero 2   | aarch64(?) |
| CM 3        | aarch64    |
| Pi 2 B v1.2 | aarch64    |
| Pi 3        | aarch64    |
| Pi 4 B      | aarch64    |

You should grab the appropriate tarball as well as sha256 and GnuPG signatures for that tarball, based on the arch available, which depends on your model (above).

**NOTE**: For up-to-date links/version you should [use the official download page](view-source:https://www.alpinelinux.org/downloads/), Raspberry Pi table.

| Arch    | Last stable directory                                                                          |
|:------- |:---------------------------------------------------------------------------------------------- |
| armhf   | [Latest stable armhf](https://dl-cdn.alpinelinux.org/alpine/latest-stable/releases/armhf/)     |
| armv7   | [Latest stable armv7](https://dl-cdn.alpinelinux.org/alpine/latest-stable/releases/armv7/)     |
| aarch64 | [Latest stable aarch64](https://dl-cdn.alpinelinux.org/alpine/latest-stable/releases/aarch64/) |

### Verify the tarball has the expected contents

See '[verify downloaded installation media](../../verify-downloaded-install-media/_index.md)'.
