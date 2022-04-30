---
date: 2022-04-28
title: Recommended tweaks and configuration
tags: ["alpine","configuration","docs","hosting","linux","self-host","sysadmin-devops"]
series: ["docs4web","alpine-linux-local-server"]
---

# Recommended tweaks and configuration

## Overview

Assuming the reboot was successful, it is time to make your system more useful.

Otherwise see [FirstbootTroubleshooting](./FirstbootTroubleshooting.md)

Commit changes at your preferred granularity
--------------------------------------------

Don't forget that these changes will not survive reboot unless you commit your changes. I like to 'commit early, commit often', but you may wish to commit less often. 

To commit, execute the following as root:

    lbu commit

Some recommended first steps
----------------------------

1. [+ConfigureSystemAndDataNetworkBackups](./RecommendedTweaksAndConfigs/ConfigureSystemAndDataNetworkBackups.md)

Some author preferences
-----------------------

### Interface / user tweaks

You may wish to implement some of these before completing 'system-related' preferences

1. [+EnableColourfulPromptForDefaultAshAndOptionalBashShells](./RecommendedTweaksAndConfigs/EnableColourfulPromptForDefaultAshAndOptionalBashShells.md)
2. [+AddManPages](./RecommendedTweaksAndConfigs/AddManPages.md)
3. [+AddTmux](./RecommendedTweaksAndConfigs/AddTmux.md)
4. [+EditMOTD](./RecommendedTweaksAndConfigs/EditMOTD.md)

### System-related

1. [+AddEtckeeper](./RecommendedTweaksAndConfigs/AddEtckeeper.md)
2. [+AddEtckeeperGitRemoteForEtcBackup](./RecommendedTweaksAndConfigs/AddEtckeeperGitRemoteForEtcBackup.md)

Useful notes and links
----------------------

* <https://wiki.alpinelinux.org/wiki/Setting_up_a_software_RAID_array> [+LocalCopyOfWikiRAIDSetupPage](./RecommendedTweaksAndConfigs/LocalCopyOfWikiRAIDSetupPage.md)
* <https://wiki.alpinelinux.org/wiki/Setting_up_a_new_user>
