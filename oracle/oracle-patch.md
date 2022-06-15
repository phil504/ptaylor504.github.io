---
layout: default
title: OPatch One-off Installation
parent: Oracle Tips
---

Notes on steps to install an oracle patch

1.  Download Patch
2.	Copy downloaded patch to location on server
    1.	For example: /tmp
3.	Unzip into directory
    1.	For example: unzip -d patching-files p26755797_122130_Generic.zip
4.	Locate the OPatch Utility
    1.	ORACLE_HOME/Opatch/
    2.	It is in same directory as wlserver
5.	Add the OPatch location to the PATH
    1.	export PATH=$PATH:/apps/path/to/oracle_home/Opatch
    2.	example: export PATH=$PATH:/u02/oracle/products/fmw/OPatch/
6.	From the location of patch
    1.	opatch -version
    2.	list the installed patches
        1.	opatch lsinentory
    3.	install the patch
        1.	opatch apply
            1.	Error: Exception occured :     fuser could not be located:
            2.	Resolution: export OPATCH_NO_FUSER=true , then re-run opatch apply.  For more info see Doc ID 2429708.1.