# RecommendedTweaksAndConfigs
Created Thursday 28 April 2022

Overview
--------

Assuming the reboot was successful, it is time to make your system more useful.

Otherwise see [FirstbootTroubleshooting](./FirstbootTroubleshooting.md)

Commit changes at your preferred granularity
--------------------------------------------

Don't forget that these changes will not survive reboot unless you commit your changes. I like to 'commit early, commit often', but you may wish to commit less often. 

To commit, execute the following as root:

	lbu commit


Some recommended first steps
----------------------------


1. [+CreateANotRootAdminUser](./RecommendedTweaksAndConfigs/CreateANotRootAdminUser.md)
2. [+ConfigureSSHForPubkeyOnly](./RecommendedTweaksAndConfigs/ConfigureSSHForPubkeyOnly.md)
3. [+UseEncryptedLBU](./RecommendedTweaksAndConfigs/UseEncryptedLBU.md)
4. [+ForHeadlessSystemsAddEntropy](./RecommendedTweaksAndConfigs/ForHeadlessSystemsAddEntropy.md)
5. [+AddPackagesForOnMountFilesystemCheck](./RecommendedTweaksAndConfigs/AddPackagesForOnMountFilesystemCheck.md)


Some author preferences
-----------------------

### System-related


1. [+AddEtckeeper](./RecommendedTweaksAndConfigs/AddEtckeeper.md)
2. [+AddEtckeeperGitRemoteForEtcBackup](./RecommendedTweaksAndConfigs/AddEtckeeperGitRemoteForEtcBackup.md)
3. [+ConfigureSystemAndDataNetworkBackups](./RecommendedTweaksAndConfigs/ConfigureSystemAndDataNetworkBackups.md)


### Interface / user tweaks

You may wish to implement some of these before completing 'system-related' preferences


1. [+AddNanoAndUseAsDefaultEditor](./RecommendedTweaksAndConfigs/AddNanoAndUseAsDefaultEditor.md)
2. [+EnableColourfulPromptForDefaultAshAndOptionalBashShells](./RecommendedTweaksAndConfigs/EnableColourfulPromptForDefaultAshAndOptionalBashShells.md)
3. [+AddManPages](./RecommendedTweaksAndConfigs/AddManPages.md)
4. [+AddTmux](./RecommendedTweaksAndConfigs/AddTmux.md)
5. [+EditMOTD](./RecommendedTweaksAndConfigs/EditMOTD.md)


Useful notes and links
----------------------


* <https://wiki.alpinelinux.org/wiki/Setting_up_a_software_RAID_array> [+LocalCopyOfWikiRAIDSetupPage](./RecommendedTweaksAndConfigs/LocalCopyOfWikiRAIDSetupPage.md)
* <https://wiki.alpinelinux.org/wiki/Setting_up_a_new_user>


