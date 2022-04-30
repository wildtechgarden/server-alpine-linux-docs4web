# GuidesForSettingKernelParameters
Created Friday 29 April 2022

Overview
--------

These vary with architecture and specific device

Linux kernel guide to its parameters
------------------------------------

<https://www.kernel.org/doc/html/latest/admin-guide/kernel-parameters.html>

A suggested tweak
-----------------

Adding ``consoleblank=300`` can be a nice addition to the kernel commandline (blanks text console if left idle for over 300 seconds (5 minutes).

### Modifying files on the boot partition

If your boot partition is mounted on ``/media/``mmcblk0p1, you need to make /media/mmcblk0p1 read-write before you can make changes. To so execute:
	mount -o remount,rw /media/mmcblk0p1

change what you need, then return to read-only status
	mount -o remount,ro /media/mmcblk0p1


Hint: Typical x86-64 systems will use ``/media/sda1`` rather than ``/media/mmcblk0``.

It is recommended that you do **not** make this partition read-write under normal conditions. This avoids accidental writes which could render your system unbootable.

Systems using Syslinux for bootloader
-------------------------------------

**WARNING:** Changing the kernel commandline or boot configuration can render your system unbootable, depending on the parameters you change.

Edit ``syslinux.cfg`` in the boot partition. For example, ``/media/sda1/boot/syslinux/syslinux.cfg``.

The default x86-64 commandline in ``syslinux.cfg``:
	APPEND modules=loop,squashfs,sd-mod,usb-storage quiet


Systems using GRUB for bootloader
---------------------------------

**WARNING:** Changing the kernel commandline or boot configuration can render your system unbootable, depending on the parameters you change.

Edit ``grub.cfg`` in the boot partition. For ``example``, ``/media/sda1/boot/grub/grub.cfg``.

The default x86-64 commandline in ``grub.cfg``:
	linux	/boot/vmlinuz-lts modules=loop,squashfs,sd-mod,usb-storage quiet 


Systems using U-boot
--------------------

TBD

Raspberry Pi
------------

### Kernel parameter setting (boot time)

**WARNING:** Changing the kernel commandline can render your system unbootable, depending on the parameters you change.

``/media/mmcblk0p1/commandline.txt`` is passed verbatim to the kernel at the end of the kernel commandline. Edit to suit your needs.

### Device-tree (config.txt/usercfg.txt)

``/media/mmcblk0p1/usercfg.txt ``-  The preferred location for setting certain hardware configuration options (see <https://gist.github.com/GrayJack/2b27cdaf9a6432da7c5d8017a1b99030> for information).
``/media/mmcblk0p1/config.txt`` is updated on kernel updates so it is recommended that you do not use this location. Instead use *usercfg.txt*. Note that some parameters like ``gpu_mem=32`` will not be honoured in 'usercfg.txt' and therefore you must edit 'config.txt' and remember to update on kernel update.


