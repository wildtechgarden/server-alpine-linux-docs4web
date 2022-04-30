# Server install & configure
Created Thursday 28 April 2022

Overview
--------

This set of guides and recommendations is aimed at the use of Alpine as your local servers on physical hardware where you have access to the console on boot. Notes for differences with headless installations (but still local) are included inline.

Cloud / production deployments remain to be added (ideally in a mature production environment one would never access an interactive shell on the server, so no SSH, no console enhancements, and no online documentation like man pages for shell users). Cloud deployment would also tend to not use the 'diskless / data' style of deployment outlined here, since one should be doing a more advanced division of OS from persistent data in that type of scenario.

Also not documented here is 'automated' installation and configuration, although likely I will be adding that based on these pages in another set of guides.

Guides
------


1. [Create data install](./ServerInstallConfig/CreateDataInstall.md)
2. [Use modified setup-alpine procedure](./ServerInstallConfig/UseModifiedSetupAlpineProcedure.md)
3. [Add essential packages](./ServerInstallConfig/AddEssentialPackages.md)
4. [Commit LBU](./ServerInstallConfig/CommitLBU.md)
5. [Reboot](./ServerInstallConfig/Reboot.md) 
6. [Kernel and hardware notes - hardware specific tweaks & configuration](./KernelAndHardwareNotes/HardwareSpecificTweaksAndConfigs.md)
7. [Recommended tweaks and configuration](./ServerInstallConfig/RecommendedTweaksAndConfigs.md)


Troubleshooting
---------------


* [First boot troubleshooting](./ServerInstallConfig/FirstbootTroubleshooting.md)

 


