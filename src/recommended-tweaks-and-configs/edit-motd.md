# EditMOTD
Created Thursday 28 April 2022

Overview
--------

The existing message of the day (MOTD) includes:

``You can setup the system with the command: setup-alpine``

``You may change this message by editing /etc/motd.``

Which is potentially confusing, or just annoying, once you have set up your system. Fortunately changing it is easy.

Configure [/etc/motd](file:///etc/motd)
---------------------------------------

Simply execute (as your non-root admin user with sudo access, in this example):

	sudoedit /etc/motd


Edir or replace the plaintext message here, save, and exit.

Commit your changes
-------------------

If you have been following along and applying this guide's recommendations:

	etckeeper commit "Change the message of the day"
	lbu commit


