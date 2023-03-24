---
date: 2022-07-09
title: "Netboot Alpine Linux using iPXE"
tags: ["alpine","howtos","linux","sysadmin-devops"]
series: ["docs4web","alpine-linux-local-server"]
pageCanonical: false
toCanonical: https://wiki.alpinelinux.org/wiki/Netboot_Alpine_Linux_using_iPXE
description: "It can be especially useful to use network booting to create virtual machines without using install media on the VM. To do that we netboot with iPXE."
summary: "It can be especially useful to use network booting to create virtual machines without using install media on the VM. To do that we netboot with iPXE."
---

## Copy the files needed by iPXE to a web server

* For this guide we will provide the files at `http://ipxe-boot.example.com/` from the directory `/var/www/ixpe-boot.example.com/` on the web server, which is writable by your non-root admin user. We also assume the web server follows symlinks within `/var/www/ipxe-boot.example.com` (but not outside that directory tree).

* Copy the netboot tarball (for example the [3.16.0 stable release of Alpine's netboot image for x86_64](https://dl-cdn.alpinelinux.org/alpine/v3.16/releases/x86_64/alpine-netboot-3.16.0-x86_64.tar.gz)) to your non-root admin user on your web server.

* Extract the netboot tarball to your webserver directory. For example:

  ```shell
  tar -C /var/www/ipxe-boot.example.com -xzf alpine-netboot-3.16.0-x86_64.tar.gz
  ```

* This will create a directory structure such as:

  ```shell
  boot/
  boot/initramfs-lts
  boot/config-virt
  boot/dtbs-virt/
  boot/System.map-lts
  boot/vmlinuz-virt
  boot/System.map-virt
  boot/config-lts
  boot/initramfs-virt
  boot/modloop-lts
  boot/modloop-virt
  boot/dtbs-lts/
  boot/vmlinuz-lts
  ```

## Create an iPXE boot script

For example, create a script called `boot.ipxe` with contents:

```shell
#!ipxe

set base-url http://ipxe-boot.example.com

kernel ${base-url}/boot/vmlinuz-virt console=tty0 modules=loop,squashfs quiet nomodeset alpine_repo=https://dl-cdn.alpinelinux.org/alpine/v3.16/main modloop=http://ipxe-boot.example.com/boot/modloop-virt
initrd ${base-url}/boot/initramfs-virt
boot
```

## Boot using the iPXE boot script

### Using QEMU (for testing)

Assuming you have the binary `qemu-system-x86_64` on your system:

```shell
qemu-system-x86_64 -boot n -m 512M -enable-kvm -device virtio-net,netdev=n1 -netdev user,id=n1,tftp=$(pwd),bootfile=/boot.ipxe
```

### Using Libvirt

* Copy the `boot.ipxe` script to your webserver at `/var/www/ipxe-boot.example.com/boot.ipxe` (substituting for your actual directory, of course).

* Create a new NAT network with XML such:

  ```xml
  <network>
    <name>ipxeboot</name>
    <forward mode="nat">
      <nat>
        <port start="1024" end="65535"/>
      </nat>
    </forward>
    <bridge name="virbr1" stp="on" delay="0"/>
    <mac address="52:54:00:a4:10:b3"/>
    <domain name="ipxeboot"/>
    <ip address="192.168.129.1" netmask="255.255.255.0">
      <dhcp>
        <range start="192.168.129.128" end="192.168.129.254"/>
        <bootp file="http://ipxe-boot.example.com/boot.ipxe"/>
      </dhcp>
    </ip>
  </network>
  ```

* Use `virt-install` such as:

  ```shell
  virt-install -n vm-name --memory 512 --vcpus 1 --pxe --disk size=5,bus=virtio --network network=ipxeboot,model=virtio --input tablet --video virtio --os-variant id=http://alpinelinux.org/alpinelinux/3.13
  ```

### On Vultr.com

*NOTE*: Other cloud providers have similar features, but I haven't used them.

[iPXE Boot Feature - Vultr.com](https://www.vultr.com/docs/ipxe-boot-feature/)

## See Also

[Alpine linux netboot server](https://boot.alpinelinux.org/)
