# SetupAPKRepositoriesToUse
Created Friday 29 April 2022

Details
-------


1. Execute ``setup-ntp # If you don't setup NTP the time may be off, resuling in failure to use HTTPS, below.``
2. Execute ``setup-apkrepos``.

  You can use ``2.``  as many times as you wish. Each time will append the repository you select in ``/etc/apk/respositories``. This allows you to have multiple mirrors in your config, in case the default one is giving you trouble.

3. Execute ``apk update``.


