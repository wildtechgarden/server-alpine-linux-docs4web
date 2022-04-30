# Install an Alpine server on a Raspberry Pi
Created Friday 29 April 2022

Motivation
----------

There are some less than stellar guides on the Alpine wiki

<https://wiki.alpinelinux.org/wiki/Raspberry_Pi>
<https://wiki.alpinelinux.org/wiki/Classic_install_or_sys_mode_on_Raspberry_Pi>

So here is an attempt at something better for a diskless/data install.

Special Notes
-------------

**NOTE:** For boot to succeed `/media/mmcblk0p1/usercfg.txt` must exist. See [Raspberry Pi kernel device-tree settings](./KernelAndHardwareNotes/HardwareSpecificTweaksAndConfigs.md) for information on what you can set in there. A blank file is sufficient to allow booting, however.

Guides
------

[Creating initial boot media](./OnRaspberryPi/CreatingInitialBootMedia.md)
[Server install and configure](./ServerInstallConfig.md)
