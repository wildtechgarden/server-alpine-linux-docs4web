# LocalCopyOfWikiRAIDSetupPage
Created Thursday 28 April 2022

Setting up a software RAID array


There are various forms of RAID: via a hardware RAID controller, "fake RAID", and "software RAID" using mdadm, which is Linux-only. These instructions discuss only the last form of RAID. Only RAID for arbitrary storage is covered here. It's possible to have one's system root /, or /var, or swap, or even one's /boot, on a RAID array. See Setting up disks manually for more details about doing any of that.
Contents

1 RAID Levels
2 Advice
3 Loading needed modules
4 Creating the partitions
5 Setting up the RAID array
6 Monitoring sync status
7 Saving config
8 Adding a RAID after the installation
9 More Info on RAID

RAID Levels

There are several "levels" of RAID to choose between:

RAID0 essentially just glues two devices together, making a larger virtual drive. Reads and writes are "striped" between the drives for speed improvements. (That is, your hardware may read from, or write different data to, multiple devices in parallel.) A "device" here is usually a partition of a hard drive.
RAID1 "mirrors" writes to two devices, for improved safety. Then if one of the devices fails, the data will still be available on the other.
RAID5 is similar to RAID1, but it uses three devices and provides the space of two of them. The data will be preserved as long as any two of the three devices continue to work.

There are other RAID levels as well. Here is an explanation of their differences.
Advice

Your /boot partition should either not be on RAID, or else be on a RAID1 array, with no further layers of encryption or LVM. (Alpine's default bootloader extlinux can't handle either. Grub2 can handle /boot being on LVM.) The usual practice is to create a small (32--100 MB) partition for /boot. That can be a mirrored (RAID1) volume, however this is just for post-init access. That way, when you write a new kernel or bootloader config file to /boot, it gets written to multiple physical partitions. During the pre-init, bootloader phase, only one of those partitions will be used (and it will be mounted read-only).
It's important to note that extlinux can't boot from partitions created with mdadm metadata version 1.2, which is the default. To be on the safe side, it's recommended to create the partition based on an older metadata version, with the --metadata=0.90 parameter for the /boot partition.
You can put swap on a RAID0 volume, but there doesn't seem to be any good reason to do so. The Linux kernel already knows how to stripe several swap partitions. So you can just devote multiple ordinary (non-RAID) partitions to swap, and get the same effect. The downside from doing either of these things is that when one of your disks fails, the system will go down. For better reliability, create a mirrored (RAID1) volume and put swap there. This will let your system keep running if one of the disks fails.
All partitions in a RAID array should be the same size.
Don't ever mount just one of the devices in a RAID1 array. If you mount it r/w, then, even if you don't explicitly write anything to the device, it may get out of sync with the unmounted device, e.g. its filesystem journal has been updated. If you ever subsequently mount the other device, or the two of them together, your data will likely become corrupted. If you have to do this, make sure you mount your device r/o. Better yet, abandon the device you didn't mount. Zero out its RAID headers, and tell mdadm that that device has failed. Then you can if you like treat it as a new disk, which you can add as a replacement to your (now degraded) original RAID array.
A mirrored RAID array (level 1 or 5) protects you against hardware failure. It doesn't protect against rm -rf /, software errors, exploits, earthquakes, fire. Don't rely on RAID as a backup strategy.
Running a mirrored RAID only provides one line of defense against drive failures. It doesn't allow you to stop thinking about them. If a device in a RAID 1 starts failing and you aren't aware of it, your data will end up just as silently corrupted as it would be if you were running one drive. You have to watch your logs.

This document was updated for Alpine 2.4.6.
Loading needed modules

Start with loading the raid1 kernel module:

modprobe raid1

Add it to /etc/modules-load.d so it gets loaded during next reboot:

echo raid1 >> /etc/modules-load.d/raid1.conf
Creating the partitions

Please read up on partition types, and why you should consider using 0xda instead of 0xfd.

I will use /dev/sda and /dev/sdb in this document but your devices may be different. To find what disks you have available, look in /proc/partitions.

Create the partitions using fdisk.

fdisk /dev/sda

I will create one single partition of type Linux raid autodetect. Use n in fdisk to create the partition and t to set type. Logical volumes will be created later. My partition table looks like this ('p' prints the partition table):

   Device Boot      Start         End      Blocks  Id System
/dev/sda1               1       17753     8388261  fd Linux raid autodetect

Use w to write and quit. Do the same with your second disk.

fdisk /dev/sdb

Mine looks like this:

   Device Boot      Start         End      Blocks  Id System
/dev/sdb1               1       17753     8388261  fd Linux raid autodetect

Alternately, if your disks are the same size (as they should be, see above) you can copy the partition table from one to the other like this:

apk add sfdisk
sfdisk -d /dev/sda | sfdisk /dev/sdb
Setting up the RAID array

Install mdadm to set up the arrays.

apk add mdadm

Create the array.

mdadm --create --level=1 --raid-devices=2 /dev/md0 /dev/sda1 /dev/sdb1


Monitoring sync status

You should now be able to see the array syncronize by looking at the contents of /proc/mdstat.

~ # cat /proc/mdstat 
Personalities : [raid1] 
md0 : active raid1 sdb1[1] sda1[0]
  8388160 blocks [2/2] [UU]
  [=========>...........]  resync = 45.3% (3800064/8388160) finish=0.3min  speed=200003K/sec

unused devices: <none>

You don't need to wait until it is fully syncronized to continue.
Saving config

Create the /etc/mdadm.conf file so mdadm knows how your RAID is set up:

mdadm --detail --scan > /etc/mdadm.conf

To make sure the raid devices start during the next reboot run:

rc-update add mdadm-raid

To use the raid array in /etc/fstab at boot, the mdadm service must be started at boot time:

rc-update add mdadm boot

rc-update add mdadm-raid boot


If you're not running Alpine from a hard disk install, use

lbu commit

as usual to save your configuration changes to your removable media.

The raid device /dev/md0 is now ready to be used with LVM or mkfs.
Adding a RAID after the installation

To add a softRAID to an already installed Alpine, you need to start with these 3 steps :


3. Loading needed modules



4. Creating the partitions



5. Setting up the RAID array


Then you have to update your initfs with the command mkinitfs.


1. Be sure /etc/mkinitfs/mkinitfs.conf contain raid which should look like this:


features="ata base ide scsi usb virtio ext4 lvm raid"


2. Update the initfs with this command


mkinitfs -c /etc/mkinitfs/mkinitfs.conf -b /
More Info on RAID

These resources may be helpful:

Arch wiki page on RAID
Arch wiki page on RAID and LVM
Arch wiki page on Converting an existing system to RAID Gentoo wiki page on the same
Gentoo Linux Wiki: RAID/Software (via archive.org)
Gentoo Linux Wiki: Software RAID Install (via archive.org)
<http://www.gentoo.org/doc/en/gentoo-x86-tipsntricks.xml#software-raid>
Gentoo Linux x86 with Software Raid and LVM2 Quick Install Guide (via archive.org)

Yannick Loth: Installing Archlinux with software raid1, encrypted filesystem and LVM2 (via archive.org)
Debian MADM FAQ (via archive.org)
Linux Documentation Project: Linux RAID FAQ
<https://access.redhat.com/knowledge/docs/en-US/Red_Hat_Enterprise_Linux/6/html/Storage_Administration_Guide/ch-raid.html>
Linux 101: Arch Linux software RAID installation guide (via archive.org)
<https://raid.wiki.kernel.org/index.php/Linux_Raid>

