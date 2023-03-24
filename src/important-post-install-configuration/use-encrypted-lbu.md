---
date: 2022-04-28
title: "Use encrypted LBU"
tags: ["alpine","howtos","docs","linux","security","sysadmin-devops"]
series: ["docs4web","alpine-linux-local-server"]
description: "Unless you need headless, or unattended reboots or power up, it is highly recommended to use an encrypted configuration backup."
summary: "Unless you need headless, or unattended reboots or power up, it is highly recommended to use an encrypted configuration backup."
---

## Overview

Unless you need headless, or unattended reboots or power up (e.g. after power loss), it is highly recommended to use an encrypted configuration backup. This protects the data while the system is down (while the system up, the need to login, and the usual user access mechanism apply, but while powered down a FAT32 partition is easily read, or even any other unencrypted partition.

If you are running headless but have an option of using a serial port on your computer during boot (instead of keyboard and monitor) then you might want to read the docs on using serial console on Alpine Linux: <https://wiki.alpinelinux.org/wiki/Enable_Serial_Console_on_Boot>.

Encrypting the config and APK partition is not supported by default by Alpine Linux at the present time, so boots would fail with that option, unless you modify the initramfs.

## Configure lbu.conf

1. Modify `/etc/lbu/lbu.conf` to look something like:

   ```shell
   # What cipher to use with -e option
   DEFAULT_CIPHER=aes-256-cbc

   # Uncomment the row below to encrypt config by default
   ENCRYPTION=$DEFAULT_CIPHER

   # Uncomment below to avoid needing 'media' option to 'lbu commit'
   # Can also be set to 'floppy'  
   LBU_MEDIA=sda2

   # Set the LBU_BACKUPDIR variable in case you prefer to save the apkovls
   # in a normal directory instead of mounting an external media.
   # LBU_BACKUPDIR=/root/config-backups

   BACKUP_LIMIT=128
   ```

   We enable encryption and a history of up to 128 ``lbu commit`` actions. While this may seem like overkill, I personally 'commit early, commit often' and want to be able to restore to a working config if a break something. In addition the history should not take up that much space, since if you have a large LBU, you are probably 'doing it wrong' for the procedure described in this documentation.

2. Move your previous backup out of the way (unless you know you won't want it back;
   you should store is somewhere protected though, as it is unecrypted).

3. Commit your changes and remove the unecrypted overlay volume (LBU file) if you haven't decided to preserve it somewhere protected.

   ```shell
   doas lbu commit -d
   ```

4. You will be prompted to enter your passphrase twice. Do so.

5. In normal use you would just

   ```shell
   doas lbu commit
   ```

   And enter you passphrase, twice.
