---
date: 2022-07-09
title: "Modifying install images"
tags: ["alpine","docs","linux","devel"]
series: ["docs4web"]
pageCanonical: false
toCanonical: https://wiki.alpinelinux.org/wiki/Testing_modified_install_images_and_packages
description: "Modifying packages that are part of the install boot, or the parameters accepted by the boot process, is more involved than modifying individual packages."
summary: "Modifying packages that are part of the install diskless boot (e.g. on install media), or the parameters that can be accepted by the boot process, is a little more involved than modifying individual packages, especially for netboot images."
---

## Overview

Modifying packages that are part of the install diskless boot (e.g. on install media), or the parameters that can be accepted by the boot process, is a little more involved than modifying individual packages, especially for netboot images. This author discovered that then when working on [feat: answerfile kernel cmdline parameter (#26) · Issues · alpine / mkinitfs · GitLab](https://gitlab.alpinelinux.org/alpine/mkinitfs/-/issues/26) an issue he opened to request / offer to develop an improvement to unattended installation by adding the option of applying a `setup-alpine` 'answerfile' automatically via netboot, by providing a URL to a new `answerfile` kernel commandline parameter.

## The easy part

* Update the list of options accepted by the installer using the kernel command line by modifying [mkinitfs](https://gitlab.alpinelinux.org/alpine/mkinitfs) `initramfs-init.in` and updating the `man` page in `mkinitfs-bootparam.7.in`.
* Install the new `mkinitfs` into one's build environment using `make install` in `mkinitfs`.
* Build a new image using `scripts/mkimage.sh` from [aports](https://gitlab.alpinelinux.org/alpine/aports) with the appropriate parameters.
* You new have an image that will accept your new parameter.

## Challenge #1

* In the case of `answerfile` an additional change needs to be make to the `firstboot` initscript, which is part of the `openrc` package.
* That means building a new `openrc` package and getting it into the generated image.
* To do that one has to point `scripts/mkimage.sh` at the package repository created when building the modified `openrc` package.
* This is sufficient for images where all the packages used during boot and install are present on the install media.

## Challenge #2 (netboot)

* For netboot, however, the process is more involved because the `openrc` package has to be downloaded from an external repository during the boot process.
* This would seem easy; one might think you one could just supply put the `packages` directory created during the `openrc` build on a web server and using the `alpine_repo=<URI_of_repo>`, but the problem is that `alpine_repo` only accepts a single repository.
* In addition the package list must be signed by a key which appears in the image (that part is easy using the `mkimage.sh` parameters).
* This means one must have include _all_ the packages netboot and install will require in the new repository.
* There is one more gotcha; One must include all the _dependencies_ for the packages in the repository or the packages will fail to install.

### One method of creating the necessary signed repository

#### Identify all the base packages needed by netboot

* In the `mkinitfs` repository issue `grep pkgs initfamfs-init.in` and make note of all the packages that may be used by the initramfs.
* In `aports`, `grep apks scripts/*`. This will identify all base packages added by the `mkimage.sh` script.
* You also need `linux-lts linux-virt wireless-regdb scanelf alpine-conf alpine-base openssl`

#### Identify all the dependencies of the base packages

* Create a file with the list of base packages on a single line, separated by spaces. For example a file named `~/base-packages.lst` containing:

  ```shell
  package1 package2 package3
  ```

* Install the package `lua-aports`

* From a package directory in a package from `aports`, issue the following command:

  ```shell
  ap recursive-deps $(cat ~/base-packages.lst) >~/base-deps.lst
  ```

#### Build all required packages

##### Create required list of package directories in `aports`

* Take the list of base packages and dependencies above and create a single file with all packages on a single line, separated by spaces. For `~/base-deps.lst` above you could do:

  ```shell
  cat ~/base-deps.lst ~/base-pkgs.lst | tr $'\n' ' ' >~/oneline-deps.lst
  ```

* From a package directory in a package from `aports`, issue the following command:

  ```shell
  ap builddirs $(cat ~/oneline-deps.lst) >~/packages-to-build.lst
  ```

##### Create a directory for the package repository

```shell
mkdir -p ~/packages/main
```

##### Add this directory to the system APK repositories

* **NOTE**: This will break things if you are not running latest (edge) Alpine in your build environment

* Assuming your user home dir is `/home/user`, then to the file `/etc/apk/repositories` add

  ```shell
  /home/user/packages/main
  ```

##### Build the packages

```shell
cd ~
for pdir in $(cat ~/packages-to-build.lst); do (cd $pdir && abuild -r -m | tee -a ~/build.log); done
```

#### Build a netboot image

From the `aports` directory:

```shell
./scripts/mkimage.sh --profile netboot --repository /home/user/packages/main
```

### Copy to your netboot server and netboot

See [Netboot Alpine Linux using iPXE](../howtos/netboot-alpine-linux-using-ipxe.md) and adjust paths as necessary.
