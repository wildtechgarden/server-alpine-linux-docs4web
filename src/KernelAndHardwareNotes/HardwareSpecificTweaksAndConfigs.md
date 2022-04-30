# HardwareSpecificTweaksAndConfigs
Created Friday 29 April 2022

Overview
--------

TBD

System with No RTC (real-time clock)
------------------------------------

Includes the Raspberry Pi family of SBC (single board computers).


1. Disable hwclock (if enabled)

	service hwclock stop
	rc-update hwclock disable boot default


2. Enable swclock

	rc-update swclock enable boot default
	service swclock start


Low entropy systems
-------------------

Includes headless Raspberry Pi systems.


1. Add and enable HAVEGED  package

	rc-update add haveged boot default
	service haveged start


Wireless
--------

TBD

Kernel commandline or device-tree / config
------------------------------------------

[KernelAndHardwareNotes:GuidesForSettingKernelParameters](./GuidesForSettingKernelParameters.md)



