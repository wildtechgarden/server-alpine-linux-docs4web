---
date: 2022-04-28
title: For headless systems, add boot entropy
tags: ["alpine","configuration","docs","hosting","linux","self-host","sysadmin-devops"]
series: ["docs4web","alpine-linux-local-server"]
---

# For headless systems, add boot entropy

## Overview

As mentioned in [Raspberry Pi - Alpine Linux](https://wiki.alpinelinux.org/wiki/Raspberry_Pi) under 'Troubleshooting: Long boot time when running headless', some systems might take an excessively long time to boot when no peripherals are attached (not only with the Pi series). In those cases it can be use to add the HAVEGED package to speed up the gathering of entropy. (FIXME: Is this still needed with 5.xx kernels?)

Install haveged
---------------

```shell
apk add haveged \
 haveged-doc # Can be omitted if you don't need/want the man page and other docs
```

Enable haveged on system startup
--------------------------------

```shell
rc-update add haveged boot default # TODO: Does enabling on boot doing anything with this setup?
```
