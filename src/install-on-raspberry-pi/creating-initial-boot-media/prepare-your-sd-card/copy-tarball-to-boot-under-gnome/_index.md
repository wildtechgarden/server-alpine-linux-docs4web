---
date: 2022-04-30
title: Copy tarball to boot under Gnome
tags: ["alpine","configuration","docs","linux","sysadmin-devops","raspberry-pi","sbc"]
series: ["docs4web","alpine-linux-local-server"]
---

# Copy tarball to boot under Gnome

## Steps

Screenshots are from GNOME but most GUI desktops are similar.

1. Select install tarball wherever you have it downloads (often in your `Downloads` directory), right-click and select 'Extract To…'
   [![File manager showing extraction of install tarball](09-file-manager-extract-install-tarball-to-boot-partition.png)](09-file-manager-extract-install-tarball-to-boot-partition.png)

2. Browse to the boot partition of the SD card
   [![Initial directory when choosing directory in which to extract install tarball](10-directory-chooser-for-extracting-install-tarball.png)](10-directory-chooser-for-extracting-install-tarball.png)

3. Select the boot partition of the SD card as extraction destination
   [![We have selected the boot partition as the destination for extracting the install tarball](11-we-have-selected-the-boot-partition-for-extracting-install-tarball.png)](11-we-have-selected-the-boot-partition-for-extracting-install-tarball.png)

4. The result will be a directory containing the boot files on the boot partition; we actually want the files in the top-level (root) of the boot partition.
   [![File manager showing directory creating boot files created in the boot partition](12-result-of-extracting-install-tarball-to-boot-partition.png)](12-result-of-extracting-install-tarball-to-boot-partition.png)

5. Therefore, select all files in the directory that was created (e.g. in the file manager, browse into the directory and press \[Ctrl-A]).
   [![File manager showing all files boot files in directory from tarball selected](13-select-all-boot-files-in-tarball-directory.png)](13-select-all-boot-files-in-tarball-directory.png)

6. Cut and paste the files into the top-level (root).
   [![File manager showing the boot files moved into the top level of the boot partition](14-cut-and-paste-the-boot-files-into-the-root-of-the-boot-partition.png)](14-cut-and-past-the-boot-files-into-the-root-of-the-boot-parition.png)

7. Remove the now extraneous extraction directory (which should be empty).
   [![File manager showing result of removing the now extraneous extraction directory](15-remove-the-extraneous-extraction-directory.png)](15-remove-the-extraneous-extraction-directory.png)
