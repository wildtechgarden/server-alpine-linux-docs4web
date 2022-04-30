# ForHeadlessSystemsAddEntropy
Created Thursday 28 April 2022

Overview
--------

TBD

Install haveged
---------------

	apk add haveged \
	 haveged-doc # Can be omitted if you don't need/want the man page and other docs


Enable haveged on system startup
--------------------------------

	rc-update add haveged boot default


