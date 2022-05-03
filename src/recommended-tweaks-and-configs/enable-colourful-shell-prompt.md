---
date: 2022-04-28
title: "Enable enhanced shell prompt"
tags: ["alpine","howtos","docs","linux","shell","sysadmin-devops"]
series: ["docs4web","alpine-linux-local-server"]
---

# Enable enhanced shell prompt

Add colour and context information to prompt.

## Overview

`/etc/profile` and the '`.sh`' scripts in `/etc/profile.d` are sourced on every invocation of the 'ash' (default Alpine/Busybox shell) as well as the 'bash' shell when launched as a login shell. This allows us to have some system-wide default configuration for these shells.

Enable the disabled color_prompt.sh snippet
-------------------------------------------

Execute:

    doas mv /etc/profile.d/color_prompt.sh.disabled /etc/profile.d/color_prompt.sh

Test it
-------

1. Do a fresh login as any interactive shell  user (SSH logins work for this). **Do not** reboot before committing your changes.
2. Observe your fancy new colour prompt.

## Commit your changes

```shell
doas lbu commit
```
