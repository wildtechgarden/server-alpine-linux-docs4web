# ObtainAndVerifyInstallTarball
Created Friday 29 April 2022

Obtain the official Alpine Linux image
--------------------------------------

### Choose tarball to download based on the model of Pi you have

Partial table of model of Raspberry Pi to Linux kernel max architecture available (where aarch64 > armv7 > armhf). armhf should be a 'safe' choice for all models, but aarch64 is preferred when possible, then armv7, then armhf.

| Model       | Arch       |
|:------------|:-----------|
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


You should grab the appropriate tarball as well as sha256 and gpg signatures for that tarball, based on the arch available, which depends on your model (above).

| Arch    | Tarball                                                                                         | sha256                                                                                                 | GPG                                                                                                 |
|:--------|:------------------------------------------------------------------------------------------------|:-------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------|
| armhf   | <https://dl-cdn.alpinelinux.org/alpine/v3.15/releases/armhf/alpine-rpi-3.15.4-armhf.tar.gz>     | <https://dl-cdn.alpinelinux.org/alpine/v3.15/releases/armhf/alpine-rpi-3.15.4-armhf.tar.gz.sha256>     | <https://dl-cdn.alpinelinux.org/alpine/v3.15/releases/armhf/alpine-rpi-3.15.4-armhf.tar.gz.asc>     |
| armv7   | <https://dl-cdn.alpinelinux.org/alpine/v3.15/releases/armv7/alpine-rpi-3.15.4-armv7.tar.gz>     | <https://dl-cdn.alpinelinux.org/alpine/v3.15/releases/armv7/alpine-rpi-3.15.4-armv7.tar.gz.sha256>     | <https://dl-cdn.alpinelinux.org/alpine/v3.15/releases/armv7/alpine-rpi-3.15.4-armv7.tar.gz.asc>     |
| aarch64 | <https://dl-cdn.alpinelinux.org/alpine/v3.15/releases/aarch64/alpine-rpi-3.15.4-aarch64.tar.gz> | <https://dl-cdn.alpinelinux.org/alpine/v3.15/releases/aarch64/alpine-rpi-3.15.4-aarch64.tar.gz.sha256> | <https://dl-cdn.alpinelinux.org/alpine/v3.15/releases/aarch64/alpine-rpi-3.15.4-aarch64.tar.gz.asc> |


### Verify the tarball has the expected contents

#### Using SHA256 (just a matching check)

TBD

#### Using GnuPG (also can verify authenticity, to a degree)

TBD

