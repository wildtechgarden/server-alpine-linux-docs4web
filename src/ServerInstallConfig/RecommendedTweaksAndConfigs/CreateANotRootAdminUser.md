# CreateANotRootAdminUser
Created Thursday 28 April 2022

Avoid operating as root, where possible
---------------------------------------

It is generally considered an administrative best practise to avoid logging in and/or operating with elevated privileges, to the extent reasonable to do so. Therefore it is a good idea to have a user is not root for most operations. In addition if, as recommended, one prevents root login over SSH one needs a user than one can SSH into, and gain temporary elevated privileges when one requires them.

Create a new user
-----------------

	adduser -g "Daniel F. Dickinson,,," newadmin newadmin


Add sudo or doas
----------------

``sudo`` is the traditional tool, `doas` comes from the *BSD world; both give elevated access. Discussing the relative merits is out of scope here.

	apk add sudo

 
OR

	apk add doas


Sudo: configure sudo to allow a group full sudo access
------------------------------------------------------

TBD (group wheel)

Add new user to root access group (wheel)
-----------------------------------------



1. First make sure the group exists


	addgroup wheel



2. Then add the user to it

 
	addgroup newadmin wheel


Login as new user and test access
---------------------------------

TBD

