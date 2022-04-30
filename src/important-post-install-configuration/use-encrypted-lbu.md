# UseEncryptedLBU

Created Thursday 28 April 2022

Overview
--------

Unless you needed headless, or unattended reboots or power up (e.g. after power loss), it is highly recommended to use an encrypted configuration backup. This protects the data while the system is down (while the system up, the need to login, and the usual user access mechanism apply, but while powered down a FAT32 partition is easily read, or even an unencrypted ext4 partition.

If you are running headless but have an option of using a serial port on your computer during boot (instead of keyboard and monitor) then you might want to read the docs on using serial console on Alpine Linux: <https://wiki.alpinelinux.org/wiki/Enable_Serial_Console_on_Boot.>

Encrypting the config and APK partition is not supported by Alpine Linux at the present time, so boots would fail with that option.

Configure lbu.conf
------------------

1. Modify ``/etc/lbu/lbu.conf`` to look something like:
   
   # what cipher to use with -e option
   
    DEFAULT_CIPHER=aes-256-cbc
   
   # Uncomment the row below to encrypt config by default
   
    ENCRYPTION=$DEFAULT_CIPHER  
   
   # Uncomment below to avoid <media> option to 'lbu commit'
   
   # Can also be set to 'floppy'
   
    LBU_MEDIA=sda2
   
   # Set the LBU_BACKUPDIR variable in case you prefer to save the apkovls
   
   # in a normal directory instead of mounting an external media.
   
   # LBU_BACKUPDIR=/root/config-backups
   
    BACKUP_LIMIT=128
   
   We enable encryption and a history of up to 128 ``lbu commit`` actions. While this may seem like overkill, I personally 'commit early, commit often' and want to be able to restore to a working config if a break something. In addition the history should take up that much space, since if you have a large LBU, you are probably 'doing it wrong'.
   
    2. Move your previous backup out of the way (unless you know you won't want it back; you should store is somewhere protected though, as it is unecrypted).

2. Commit your changes
   
    lbu commit -d
   
   You will be prompted to enter your passphrase twice. Do so.
