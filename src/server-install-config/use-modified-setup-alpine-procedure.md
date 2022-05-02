---
date: 2022-04-28
title: Use modified 'setup-alpine' procedure
tags: ["alpine","configuration","docs","hosting","linux","self-host","sysadmin-devops","raspberry-pi","sbc"]
series: ["docs4web","alpine-linux-local-server"]
---

# Use modified 'setup-alpine' procedure

## Overview

You'll want to be careful during the LBU configuration and APK cache configuration sections using the default ``setup-alpine`` script. You also need to have pre-mounted the partition(s) that will hold the LBU and APK cache (see [Create semi-data/semi-diskless install](create-semi-data-install/#add-a-and39configand39-partition)).

Use 'setup-alpine', cautiously
----------------------------

Some steps (like setting up the network) will have the answers you previously gave. This can save typing if you want to keep the same answer, but if you wish to change your answers, you can.

After setting up (or disabling) SSH you should see a prompt asking if you want to use  your boot partition to store your configuration: You should say no to that prompt.

At the next prompt, the default option of those presented should be the config partition you created and mounted earlier (examples: `mmcblk0p2` or `sda2`).  If so, just press the \[ENTER] key at this prompt. If not enter the config partition you created (the `mmcblk0p2` or `sda2` examples, above) and then the \[ENTER] key.

Now you should be at a shell prompt and should [commit your settings to the LBU (configuration store, which will be located on your config partition)](commit-lbu.md).

## Alternatively use automation or a more manual setup

* [Automated installation](https://docs.alpinelinux.org/user-handbook/0.1a/Installing/setup_alpine.html#_answer_files) is another option, and can save a great deal of time when you are installing many similar systems.
* [Semi-automatic installation](https://docs.alpinelinux.org/user-handbook/0.1a/Installing/manual.html) can be a good choice, especially when first figuring out how you wish the system to be configured.
* 
