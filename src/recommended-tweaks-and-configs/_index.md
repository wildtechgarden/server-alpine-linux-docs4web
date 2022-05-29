---
date: 2022-04-28
title: Recommended tweaks and configuration
tags: ["alpine","configuration","docs","hosting","linux","self-host","sysadmin-devops"]
series: ["docs4web","alpine-linux-local-server"]
---

# Recommended tweaks and configuration

## Overview

Assuming the reboot was successful, it is time to make your system more useful.

Otherwise see [Firstboot troubleshooting](../server-install-config/firstboot-troubleshooting.md)

## Commit changes at your preferred granularity

Don't forget that these changes will not survive reboot unless you commit your changes. I like to 'commit early, commit often', but you may wish to commit less frequently.

To commit, execute the following as your non-root admin user (if you installed `sudo` rather than `doas`, use `sudo` where we write `doas`) after completing some configuration:

``` shell
doas lbu commit
```

## Some author preferences for interface / user tweaks

1. [Enable colourful and enhanced shell prompt](enable-colourful-shell-prompt.md)
2. [Add tmux](add-tmux.md)
3. [Edit message of the day (MOTD)](edit-motd.md)

## Main recommendation

[Configure automatic off-system backups](configure-off-system-backups.md)

## See also various HowTo documents

There are [a variety of howto guides in this repo](../howtos/_index.md) which you may wish to consider as well.
