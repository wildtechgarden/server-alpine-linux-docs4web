---
date: 2022-04-28
title: For headless systems, add boot entropy
tags: ["alpine","linux","self-host","sysadmin-devops"]
series: ["docs4web","alpine-linux-local-server"]
description: "Some systems might take an excessively long time to boot when no peripherals are attached. In those cases, add the rng-tools package."
summary: "Some systems might take an excessively long time to boot when no peripherals are attached (not only with the Pi series). In those cases it may be useful to add the rng-tools package to speed up the gathering of entropy."
---

As mentioned in [Raspberry Pi - Alpine Linux](https://wiki.alpinelinux.org/wiki/Raspberry_Pi) under 'Troubleshooting: Long boot time when running headless', some systems might take an excessively long time to boot when no peripherals are attached (not only with the Pi series). In those cases it may be useful to add the rng-tools package to speed up the gathering of entropy.

## Do the install

See [low entropy systems hardware-specific tweaks](../kernel-and-hardware-notes/hardware-specific-tweaks-configs.md#low-entropy-systems)

## Don't forgot to commit your changes

Otherwise they will be lost on reboot.

```shell
lbu commit
```
