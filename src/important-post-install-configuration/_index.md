---
date: 2022-04-29
title: Important post-install configuration
tags: ["alpine","configuration","linux","self-host","sysadmin-devops"]
series: ["docs4web","alpine-linux-local-server"]
description: "The following are not part of the base install, but either can be essential to system function or are widely accepted best practices."
summary: "The following are not part of the base install, but either can be essential to system function (like adding boot entropy for some headless systems like the Raspberry Pi) or are widely accepted best practices (like creating a non-root admin user and limiting time spent as root)."
---

## Overview

The following are not part of the base install, but either can be essential to system function (like adding boot entropy for some headless systems like the Raspberry Pi) or are widely accepted best practices (like creating a non-root admin user and limiting time spent as root).

## Configuration

1. [For headless systems, add entropy](for-headless-systems-add-entropy.md)
2. [Create a non-root admin user](create-a-non-root-admin-user.md)
3. [Configure SSH for non-root public key access only](configure-ssh-for-pubkey-only.md)
4. [Add packages for pre-mount filesystem checks](add-packages-for-pre-mount-filesystem-check.md)
5. [Use encrypted LBU (not applicable to 'sys' installs)](use-encrypted-lbu.md)
