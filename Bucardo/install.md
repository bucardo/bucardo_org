---
title: Bucardo install
permalink: /Bucardo/install/
---

This page describes the **bucardo install** command, which creates the Bucardo master database. For instructions on how to install the Bucardo software itself onto your system, please see [Bucardo/Installation](/Bucardo/Installation "wikilink")

__NOTOC__

Once the software is installed, the next step getting Bucardo up and running is to install a Bucardo master database. This will contain all the information Bucardo uses to run, such as the tables, databases, and syncs. Usage is simply:

` bucardo install`

Before attempting to run this, you must have a running Postgres database available, and the language Pl/PerlU must be available for creating. For systems installed via packaging, a 'plperl' package can be installed, using something similar to one of these:

`yum install postgresql-plperl`
`# or`
`apt-get install postgresql-plperl-9.1`

Once you run the install, you will be provided with a menu of options. To change them, simply enter the number, then type in the new value. When all looks good, type the letter **P** to proceed. The menu will look similar to this:

` Current connection settings:`
` 1. Host:          `<none>
` 2. Port:          5432`
` 3. User:          postgres`
` 4. Database:      postgres`
` 5. PID directory: /var/run/bucardo`
` Enter a number to change it, P to proceed, or Q to quit: `

(You can force the installation to proceed without any prompting by using the **--batch** option. The settings can also be specified on the command line: host with **--dbhost**, port with **dbport**, and the PID directory with **--piddir**.)

As part of the installation, a superuser named bucardo will be created, along with a random password. This password will be added to the current user's **.pgpass** file in their home directory.

If all goes well at this point, Bucardo is installed.

TIP: If you run into errors during install or in subsequent steps, the best thing to do is to completely remove the bucardo-owned objects and start fresh with the 'bucardo install' step. This includes doing a cascaded drop of the 'bucardo' schema and the 'bucardo' role. This should completely remove any traces of Bucardo and allow you to run the installation step cleanly again.

Please email the general mailing list (bucardo-general@bucardo.org) with any problems you encounter. Feel free to edit this page as well.

### Next steps

Once the install is complete, you should review the current configuration settings and adjust them as needed. To view them all, run:

` bucardo show all`

To adjust a particular item, just use **bucardo set x=y**, for example:

` bucardo set log_level=verbose`

Once that looks good, you should use the [add_database](/Bucardo/add_database "wikilink") command to teach Bucardo about any databases used in your replication.

### See also:

-   [Software installation](/Bucardo/Installation "wikilink")
-   [add_database](/Bucardo/add_database "wikilink")
-   [Upgrading](/Bucardo/upgrading "wikilink")
