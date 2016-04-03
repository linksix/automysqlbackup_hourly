automysqlbackup_hourly
======================

This script is an extension of [automysqlbackup]:https://sourceforge.net/projects/automysqlbackup/, 
to support hourly backups of your MySQL databases.

Compatibility
-------------

Debian and Ubuntu only. Tested on production servers with Debian 8 (Jessie) and Ubuntu 14.04.

Installation
------------

The automysqlbackup_hourly script should be copied into /etc/cron.hourly/, and
for ensure that is executable : chmod +x /etc/cron.hourly/automysqlbackup_hourly
automysqlbackup *must* be installed.
For testing it, just launch as root : ./automysqlbackup_hourly
Then, in your backup's directory, you'll see :
      hourly daily weekly monthly

Every hour, you'll have a new dump for each database in hourly directory.

How it works
------------

Every hour, it takes the last dump present in your daily or weekly directory
(depending on the day given by DOWEEKLY parameter), and move it to the
hourly/yourdb directory. Then, it launches the automysqlbackup script to
create a new dump in daily or weekly directory.
Finally, dumps older than 7 days in hourly directory are deleted. You can
change the number of days by changing ROTATION_DAYS variable, at the beginning
of the script.