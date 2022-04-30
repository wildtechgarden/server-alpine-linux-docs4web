# AddPackagesForOnMountFilesystemCheck

Created Thursday 28 April 2022

Overview
--------

TBD

Install vfat (fat32) and ext4 checkers
--------------------------------------

    apk add dosfstools \
     e2fsprogs \
     dosfstools-doc # Optional if you don't need/want the man page or other docs \
     e2fsprogs-docs # Likewise

Enable localmount on boot and default runlevels
-----------------------------------------------

    rc-update add localmount boot default
