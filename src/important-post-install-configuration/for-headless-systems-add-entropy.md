---
date: 2022-04-28
title: For headless systems, add boot entropy
tags: ["alpine","configuration","docs","hosting","linux","self-host","sysadmin-devops"]
series: ["docs4web","alpine-linux-local-server"]
---

# For headless systems, add boot entropy

## Overview

As mentioned in [Raspberry Pi - Alpine Linux](https://wiki.alpinelinux.org/wiki/Raspberry_Pi) under 'Troubleshooting: Long boot time when running headless', some systems might take an excessively long time to boot when no peripherals are attached (not only with the Pi series). In those cases it may be useful to add the HAVEGED package to speed up the gathering of entropy. (REVIEW: Is this still needed with 5.xx kernels?)

Install haveged
---------------

```shell
apk add haveged
```

Enable haveged on system startup
--------------------------------

```shell
rc-update add haveged default
```

We don't enable during the 'boot' stage because it would have no effect for our hybrid install, data installs, or diskless installs.

## Don't forgot to commit your changes

Otherwise they will be lost on reboot.

```shell
lbu commit
```
