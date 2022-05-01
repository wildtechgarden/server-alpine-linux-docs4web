---
date: 2022-05-01
title: Verify downloaded installation media
tags: ["alpine","configuration","docs","linux","security","sysadmin-devops","raspberry-pi","sbc"]
series: ["docs4web","alpine-linux-local-server"]
---

# Verify downloaded installation media

You should grab the appropriate install media as well as sha256 and GnuPG signatures for that media.

**NOTE**: For up-to-date links/version you should [use the official download page](view-source:https://www.alpinelinux.org/downloads/) download table appropriate for your device.

## Verify the tarball has the expected contents

### Using SHA256

Just a matching check (i.e. correct download contents)

#### Linux

```shell
sha256sum -c install-tarball-name.sha256
```

#### Mac OS

TBD

#### Windows 10 (PowerShell)

```powershell
(Get-FileHash 'install-tarball-name').Hash -eq (Get-Content .\install-tarball-name.sha256)
```

### Using GnuPG

Also can verify authenticity, to a degree

#### Make sure GnuPG (gpg command) is installed

##### Linux

Assuming GnuPG is installed (FIXME: usual for a desktop and many server distributions, but not Alpine unless you add it?).

##### Mac OS

You will need to install GnuPG first. See [GnuPG - Download](https://www.gnupg.org/download/) and pick a Windows version. You could also use Homebrew or other add-on package managers for Mac OS.

##### Windows

You will need to install GnuPG first. See [GnuPG - Download](https://www.gnupg.org/download/) and pick a Windows version. You could also use a package manager for windows such as Chocolatey or Scoop.

Make sure location of `gpg.exe`  is in your `PATH`

#### Make sure you have the public key with which the tarball is signed

```shell
gpg --recv-keys --keyserver keyserver.ubuntu.com 0482D84022F52DF1C4E7CD43293ACD0907D9495A
```

which is also available at <https://alpinelinux.org/keys/ncopa.asc> although getting a signing key from the same site as the signature one is verifying rather defeats the purpose, in my view.

#### Check the tarball matches the signature

```shell
gpg --verify name-of-tarball.asc name-of-tarball
```

Where `name-of-tarball` includes the `.tar.gz`

You will probably get a warning the signing key is untrusted. This is normal. Unfortunately the 'Web of Trust' that would have made that failing check useful has failed to materialize in any meaningful way.
