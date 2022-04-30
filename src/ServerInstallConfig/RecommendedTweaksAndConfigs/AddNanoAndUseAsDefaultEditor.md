# AddNanoAndUseAsDefaultEditor
Created Thursday 28 April 2022

Overview
--------

For many users ``vi`` (the default editor for Alpine) is difficult and confusing to use. Even if that is not the case for you, if you find it helpful to have the same experience as newbies you wish to help, you might implement this for your own use as well.

As usual, commands below are to be executed as root.

Install nano
------------

	apk add nano


Add a profile snippet to make nano the default editor
-----------------------------------------------------

This change will apply to 'sh' (ask/bash/dash/etc) shells that are login shells, or subhsells of a login shell. That means you will need to logout and log back in to see the effects of enabling this (or conversely disabling it).


1. Create ``/etc/profile.d/default_editor.sh`` with the following contents:

	EDITOR=nano
	export EDITOR


2. If using ``etckeeper``, now is a good time to execute:

	etckeeper commit "Make nano the default editor system-wide"


