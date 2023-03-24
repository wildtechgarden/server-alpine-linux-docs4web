---
date: 2022-04-28
title: "restic/rest-server install & configure"
tags: ["alpine","configuration","linux","sysadmin-devops"]
series: ["docs4web","alpine-linux-local-server"]
draft: true
---

``` shell
apk add rest-server \
  rest-server-doc # Optional
```

## Set command line params via `/etc/conf.d/rest-server`

See docs at `/usr/share/doc/rest-server/README.md`  
or from the rest-server github repo: <https://github.com/restic/rest-server>.

```shell
addgroup -S rest-server # adduser -S does not autocreate a group
adduser -S -h /var/lib/rest-server -g "Restic REST server,,," -D rest-server rest-server
```

Edit `/etc/conf.d/rest-server` to add

```shell
REST_USER=rest-server
REST_GROUP=rest-server
```

And configure `REST_SERVER_PATH` and any additional options (`REST_SERVER_OPTS`)

## Enable on start up

```shell
rc-update add rest-server
```

## Start it immediately

```shell
service rest-server start
```

## To manage the `htpasswd` file use `apache2-utils`

```shell
apk add apache2-utils
htpasswd …
```
