---
date: 2022-04-29
title: Setup network required for package installation
tags: ["alpine","configuration","docs","hosting","linux","network","self-host","storage","sysadmin-devops","raspberry-pi","sbc"]
series: ["docs4web","alpine-linux-local-server"]
---

# Setup network required for package installation

## Overview

TBD

Use Alpine Linux setup sub-scripts for network/DNS
--------------------------------------------------

1. Execute `setup-keymap` # To make sure you can successfully do keyboard input
2. Execute `setup-hostname`.
3. Execute `setup-interfaces`.
4. Execute `ifup eth0` # Or the appropriate interface for your system.
5. Execute `setup-dns` (if not using DHCP).

## Use Alpine Linux setup sub-script get setup network time

* Execute `setup-ntp` # If you don't setup NTP the time may be too different from internet hosts, resulting in failure attempting to use HTTPS, below.

## Use Alpine Linux setup sub-script to enable package repos

* Execute `setup-apkrepos`.
  
  You can use this as many times as you wish. Each time will append the repository you select in `/etc/apk/respositories`. This allows you to have multiple mirrors in your configuration, in case the default one is giving you trouble.

* Execute `apk update`.

* You are now ready to install the needed packages.
