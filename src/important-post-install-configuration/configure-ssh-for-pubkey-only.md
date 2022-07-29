---
date: 2022-04-28
title: "Configure SSH to only allow pubkey logins"
tags: ["alpine","howtos","docs","linux","security","sysadmin-devops"]
series: ["docs4web","alpine-linux-local-server"]
description: "Disallowing SSH login with only a username and password is a well known security best practise, therefore we implement it."
summary: "Disallowing SSH login with only a username and password is a well known security best practise, therefore we implement it."
---

## Overview

Disallowing SSH login with only a username and password is a well known security best practise, therefore we implement it.

## Add a public key to your non-root admin user

In our examples we have been using the username `newadmin`.

1. If you do not already have an SSH keypair or SSH keypairs on the host(s) from which you will be connecting to this Alpine server as this non-root admin user, you should generate one now.  
   Here are some guides on how to do that.

    * [How Do I Generate SSH Keys? - Vultr.com](https://www.vultr.com/docs/how-do-i-generate-ssh-keys/)
    * [Connecting to GitHub with SSH - GitHub Docs](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)
    * [Scaleway's Guide for SSH key generation](https://www.scaleway.com/en/docs/console/my-project/how-to/create-ssh-key/)
    * [Creating and connecting to your first Public Cloud instance | OVH Guides](https://docs.ovh.com/gb/en/public-cloud/public-cloud-first-steps/#step-1-creating-ssh-keys)

2. On the server, logged in as `newadmin`
3. `cd ~` (Make sure you are in the base of your home directory)
4. `chmod 0700 .` (Make the home directory accessible only by `newamdin`)
5. `mkdir p -m 0700 .ssh` (Make the standard directory for holding SSH keys, and make it accessible only by `newadmin`, if the directory does not already exist).
6. `cd .ssh`
7. `touch authorized_keys` (Make an empty file (`authorized_keys`) for public keys that are accepted for login, if the file does not already exist).
8. `chmod 0600 authorized_keys` (Make the `authorized_keys` file accessible only by `newadmin` and the SSH server).
9. Add your public key, which you generated above, to `authorized_keys`. You can add as many as you wish, one per line.

## Verify login

1. In a new terminal on the host which will be accessing `newadmin` on this server, SSH to the server as `newadmin`. E.g. `ssh newadmin@your-alpine-server.example.com` (assuming you ssh private key was created in default location for the user from which you are issuing this command). You may be prompted for the password for the key. If so enter it. To minimize the need to enter the password to decrypt your private key, reads on on `ssh-agent` and how to enable it for your host.
2. You should be logged without having entered the password for the `newadmin` user (unless you have done something foolish like use the same password for your SSH private key).

## Configure sshd_config to prevent root login

Edit `/etc/ssh/sshd_config` and change `PermitRootLogin` to

```shell
PermitRootLogin no
```

## Configure sshd_config to prevent password and keyboard-interactive logins

Edit `/etc/ssh/sshd_config` and change `PasswordAuthencation` and `KbdInteractiveAuthentication` to

```shell
PasswordAuthentication no
KbdInteractiveAuthentication no
```

## Test config to verify it is not broken

Execute

```shell
doas sh -c 'sshd -t -f /etc/ssh/sshd_config; echo $?'
```

There should be no errors and and digit "0" should be the output of the command.

If there are errors fix them before restarting the server or you will no longer have access via SSH.

## Restart SSH server

```shell
doas service sshd restart
```

## Test login

Before logging out of your current session, make sure logging in succeeds by starting another SSH session in another terminal.

If it doesn't you need to figure out what is wrong or you will only have local access.

## Don't forgot to commit your changes

Otherwise they will be lost on reboot.

```shell
doas lbu commit
```
