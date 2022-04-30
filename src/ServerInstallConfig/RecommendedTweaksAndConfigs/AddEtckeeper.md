# AddEtckeeper
Created Thursday 28 April 2022

Overview
--------

While the LBU mechanism with backups allows restoring to previous state it lacks commented history. Done right, etckeeper will lead to a better record of what changes you made to the configuration and why, which improves your ability to recreate what you did, as well as understand why you did what you did. It also makes it easier to revert broken changes in a more granular fashion.

Configure Git for the root user
-------------------------------

This is known as a 'global' configuration as 'local' configuration refers to per-repository configuration.

The following command should be run as root (e.g. prefixed with ``sudo `` or doas  when in your admin non-root user account).


1. Make sure apk package list is up to date

	apk update


2. Add ``git``

	apk add git


3. Execute the following commands as root, adjusted to suit you and your preferences

	git config --global init.defaultBranch main
	git config --global user.name "root@yourserver (Daniel F. Dickinson)" # Obviously you want your name here
	git config --global user.email "dfdpublic@wildtechgarden.ca" # Obviously you want your email here
	git config --global pull.ff only
	git config --global core.fileMode true
	git config --global core.eol lf
	git config --global core.autocrlf false
	git config --global core.editor nano


4. Repeat for you non-root admin user (*without* ``sudo``), adjusted to suit your preferences. (Etckeeper uses the configured ``user.name`` and ``user.email`` of the original user (e.g. the ``sudo``-ing user for non-root admin ``sudo``-ing to ``root``) to set the author and comitter fields, so you need to set at least ``user.email`` and ``user.name`` for each user that will be using ``etckeeper``, even if through ``sudo``). 


Install and configure etckeeper
-------------------------------


1. Install etckeeper

	apk add etckeeper


2. Edit ``/etc/etckeeper/etckeeper.conf`` so it has the following snippets in place of the defaults for these items:
	1. Don't autocommit every day; this just creates noise if we are doing things right

	AVOID_DAILY_AUTOCOMMITS=1


2. Just avoids a warning that doesn't help us much

	AVOID_SPECIAL_FILE_WARNING=1


3. This will require to use ``etckeeper commit "A message about the commit"`` before installing with APK, if there are changes to ``/etc`` you have not already committed. This makes the logs more useful than the automatic messages that let one be too careless.

	AVOID_COMMIT_BEFORE_INSTALL=1 


3. Add root's ``.gitconfig`` to LBU backups

	lbu add /root/.gitconfig


4. If your non-root admin user(s) home(s) are not on persistent storage, add those ``.gitconfig`` to LBU as well.


Commit your changes
-------------------

1. Commit changes to ``etckeeper``

	etckeeper commit "Configure etckeeper"


2. Commit the changes to LBU (not strictly necessary if you will be doing other changes before committing; just *don't forget* to commit to LBU).

	lbu commit


