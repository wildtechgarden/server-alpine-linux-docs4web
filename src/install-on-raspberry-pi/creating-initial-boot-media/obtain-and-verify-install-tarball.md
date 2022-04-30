---
date: 2022-04-29
title: Obtain and verify install tarball
tags: ["alpine","configuration","docs","linux","security","sysadmin-devops","raspberry-pi","sbc"]
series: ["docs4web","alpine-linux-local-server"]
---

# Obtain and verify install tarball

Obtain the official Alpine Linux image
--------------------------------------

### Choose tarball to download based on the model of Pi you have

Partial table of model of Raspberry Pi to Linux kernel max architecture available (where aarch64 > armv7 > armhf). armhf should be a 'safe' choice for all models, but aarch64 is preferred when possible, then armv7, then armhf.

| Model       | Arch       |
|:----------- |:---------- |
| Pi A        | armhf      |
| Pi B        | armhf      |
| Pi 2 A      | armhf      |
| Pi B+       | armhf      |
| Pi Zero     | armhf      |
| Pi Zero W   | armhf      |
| Pi 2 B      | armv7      |
| Pi Zero 2   | aarch64(?) |
| CM 3        | aarch64    |
| Pi 2 B v1.2 | aarch64    |
| Pi 3        | aarch64    |
| Pi 4 B      | aarch64    |

You should grab the appropriate tarball as well as sha256 and GnuPG signatures for that tarball, based on the arch available, which depends on your model (above).

**NOTE**: For up-to-date links/version you should [use the official download page](view-source:https://www.alpinelinux.org/downloads/), Raspberry Pi table.

| Arch    | Last stable directory                                                                          |
|:------- |:---------------------------------------------------------------------------------------------- |
| armhf   | [Latest stable armhf](https://dl-cdn.alpinelinux.org/alpine/latest-stable/releases/armhf/)     |
| armv7   | [Latest stable armv7](https://dl-cdn.alpinelinux.org/alpine/latest-stable/releases/armv7/)     |
| aarch64 | [Latest stable aarch64](https://dl-cdn.alpinelinux.org/alpine/latest-stable/releases/aarch64/) |

### Verify the tarball has the expected contents

#### Using SHA256

Just a matching check (i.e. correct download contents)

##### Linux

```shell
sha256sum -c install-tarball-name.sha256
```

##### MacOS

TBD

##### Windows 10 (PowerShell)

```powershell
(Get-FileHash 'install-tarball-name').Hash -eq (Get-Content .\install-tarball-name.sha256)
```

#### Using GnuPG

Also can verify authenticity, to a degree

##### Make sure GnuPG (gpg command) is installed

###### Linux

Assuming GnuPG is installed (FIXME: usual for a desktop and many server distributions, but not Alpine unless you add it?).

###### MacOS

You will need to install GnuPG first. See [GnuPG - Download](https://www.gnupg.org/download/) and pick a Windows version. You could also use Homebrew or other add-on package managers for MacOS.

###### Windows

You will need to install GnuPG first. See [GnuPG - Download](https://www.gnupg.org/download/) and pick a Windows version. You could also use a package manager for windows such as Chocolatey or Scoop.

Make sure location of `gpg.exe`  is in your `PATH`

##### Make sure you have the public key with which the tarball is signed

```shell
gpg --recv-keys --keyserver keyserver.ubuntu.com 0482D84022F52DF1C4E7CD43293ACD0907D9495A
```

which is also available at <https://alpinelinux.org/keys/ncopa.asc> although getting a signing key from the same site as the signature one is verifying rather defeats the purpose, in my view.

##### Check the tarball matches the signature

```shell
gpg --verify name-of-tarball.asc name-of-tarball
```

where `name-of-tarball` includes the `.tar.gz`

You will probably get a warning the signing key is untrusted. This is normal. Unfortunately the 'Web of Trust' that would have made that failing check useful has failed to materialize in any meaningful way.
