# Prepare your SD card

Created Friday 29 April 2022

Overview
--------

Partition the SD card
---------------------

### On Windows 10

#### Using built-in GUI 'Disk Management' feature

#### Using diskpart

#### Using PowerShell

### On Linux (many distros)

#### Using Gnome 'Disks' applet

[![Gnome Disks showing an empty, unpartitioned SD card](01-gnome-disks-empty-sd-card.png)](01-gnome-disks-empty-sd-card.png)

[![Gnome Disks while adding a primary partition](02-gnome-disks-add-boot-partition.png)](02-gnome-disks-add-boot-partition.png)

[![Gnome Disks add parition wizard format as vfat](03-gnome-disks-format-boot-as-vfat.png)](03-gnome-disks-format-boot-as-vfat.png)

[![Gnome Disks showing SD card with FAT 16 boot partition](04-gnome-disks-sd-card-with-boot-partition.png)](04-gnome-disks-sd-card-with-boot-partition.png)

[![Gnome Disks setting partition as bootable](05-gnome-disks-make-partition-bootable.png)](05-gnome-disks-make-partition-bootable.png)

[![Drop to terminal to reformat as FAT 32 because GNOME disks doesn't have that option](06-terminal-reformat-as-fat32.png)](06-terminal-reformat-as-fat32.png)

[![Gnome Disks showing boot parition formatted as FAT 32](07-gnome-disks-sd-card-with-fat32-boot-partition.png)](07-gnome-disks-sd-card-with-fat32-boot-partition.png)

[![Gnome Disks showing boot partition mounted](08-gnome-disks-sd-card-mounted-boot-partition.png)](08-gnome-disks-sd-card-mounted-boot-partition.png)

#### Using CLI parted

#### Using CLI fdisk

### On MacOS

TBD

Copy the tarball contents to 'boot' partition
---------------------------------------------

### On Windows 10

### On Linux (many distros)

#### GUI (GNOME)

Screenshots are from GNOME but most GUI desktops are similar.

[![File manager showing extraction of install tarball](09-file-manager-extract-install-tarball-to-boot-partition.png)](09-file-manager-extract-install-tarball-to-boot-partition.png)

[![Initial directory when choosing directory in which to extract install tarball](10-directory-chooser-for-extracting-install-tarball.png)](10-directory-chooser-for-extracting-install-tarball.png)

[![We have selected the boot partition as the destination for extracting the install tarball](11-we-have-selected-the-boot-partition-for-extracting-install-tarball.png)](11-we-have-select-the-boot-partition-for-extracting-install-tarball.png)

[![File manager showing directory creating boot files created in the boot partition](12-result-of-extracting-install-tarball-to-boot-partition.png)](12-result-of-extracting-install-tarball-to-boot-partition.png)

[![File manager showing all files boot files in directory from tarball selected](13-select-all-boot-files-in-tarball-directory.png)](13-select-all-boot-files-in-tarball-directory.png)

[![File manager showing the boot files moved into the top level of the boot partition](14-cut-and-paste-the-boot-files-into-the-root-of-the-boot-partition.png)](14-cut-and-past-the-boot-files-into-the-root-of-the-boot-parition.png)

[![File manager showing result of removing the now extraneous extraction directory](15-remove-the-extraneous-extraction-directory.png)](15-remove-the-extraneous-extraction-directory.png)

### On MacOS

TBD
