---
date: 2022-04-28
title: "Add man pages and other on-system docs"
tags: ["alpine","howtos","docs","linux","sysadmin-devops"]
series: ["docs4web","alpine-linux-local-server"]
---

# Add man pages and other on-system docs

Overview
--------

Unless you have packages that are 'expensive' either in terms of the memory they use while operating or in terms of the amount space they take up (since in Alpine 'data' (and in 'diskless') mode packages are stored in RAM while the system is booted) you should have plenty of available RAM and storage to add the online documentation (mostly in the form of ``man`` pages).

Online documentation is optional but it makes life a heck of a lot easier, especially if one is at a physical console of a CLI-only system and thus searching web pages for answers is therefore impractical.

Add the man page command and base man pages
-------------------------------------------

Execute (as root):

```shell
    apk add mandoc mandoc-doc mandoc-apropos man-pages
```

Add man pages for packages already on system
--------------------------------------------

This will vary depending on what you have installed at this point. Here is an example command (as root):

    apk add apk-tools-doc \
     busybox-doc \
     chrony-doc \
     f2fs-tools-doc \
     etckeeper-doc \
     findutils-doc \
     fstrm-doc \
     git-doc \
     haveged-doc \
     ifupdown-ng-doc \
     iproute2-doc \ 
     lvm2-doc \
     nano-doc \
     openssh-doc \
     openssl3-doc \
     sudo-doc
