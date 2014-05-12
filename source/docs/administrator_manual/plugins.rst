Plugins and hooks
*****************

There is a possibility to customize GIS.lab installation using *plugins* and *account hooks*.
All of them are automatically loaded at installation process or in case of *account hooks*, when when particular action is triggered.

Server plugins
--------------
*Server plugin* is a script with assigned executable permissions.
It is executed after GIS.lab server installation or upgrade, before user accounts creation.

Location: user/plugins/server'

Actions:

 * install: when initial server installation is performed

 * upgrade: when server upgrade is performed

Client plugins
--------------
*Client plugin* is evaluated as LTSP plugin script (see https://wiki.edubuntu.org/HowtoWriteLTSP5Plugins).
Client plugins are "sourced" not "executed", so be careful to avoid such things as "exit" in your plugin scripts.
Files must not have executable permissions set.

Location: user/plugins/client

Actions:

 * commandline: builds the list of commandline arguments supported by the loaded plugins  

 * configure: sets variables for commandline options that are set
 * before-install: before the initial chroot is built

 * install: where the initial chroot is built (debootstrap, on debian systems)

 * after-install: additional package installation(ltsp-client), tweaks, etc.

 * finalization: the last steps needed, such as installing kernels, copying the kernels and network bootable images into the tftp dir, installing the server's ssh keys into the chroot, etc.

Variables:

 * $ARCH - the servers architecture

 * $BASE - the basic directory used for ltsp chroots (defaults to /opt/ltsp)

 * $CHROOT - the name of the chroot we create in the $BASE dir (by default substituted with $ARCH)

 * $ROOT - will always point to the client dir (/opt/ltsp/$CHROOT), use it where appropriate

To execute a command in client chroot start it with 'chroot $ROOT' command.


Account hooks
-------------
*Account hook* is a script with assigned executable permissions. It is when new user account is created or removed.

Location: user/plugins/account

Actions:

 * add - when user account is created

 * remove - when user account is removed
