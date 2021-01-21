---
title: Bucardo Command Line Tool
---

**bucardo** is the main interface to Bucardo - it is used to start, stop, and control Bucardo.

You can tell `bucardo` where to find the main [Bucardo database](/Bucardo/Bucardo_database) by use of the following arguments:

- --dbport
- --dbhost
- --dbname
- --dbuser

Additional bucardo arguments include:

- --quiet=0
- --verbose=0
- --bcverbose=1
- --sendmail=0
- --extraname=''
- --debugfilesep=0
- --debugdir='.'
- --debugname=''
- --debugsyslog=1 _Enables/Disables Syslog_
- --debugfile=1    _Enables/Disables local log file ./log.bucardo_
- --cleandebugs=0

Rather than enter those every time, you may place the arguments into a [bucardorc](/Bucardo/configuration/bucardorc) file. All of the arguments below, except for "install", require that enough options exist to find the main Bucardo database.

### Installing and upgrading Bucardo

-    To install Bucardo for the first time, see the [Bucardo installation](/Bucardo/installation/) page.
-    To upgrade Bucardo, See the [Bucardo upgrade](/Bucardo/installation/upgrade) page.

### Controlling Bucardo

#### Starting Bucardo

To start Bucardo, simply enter:

    bucardo start "Reason for starting"

The reason is optional but recommended.

#### Stopping Bucardo

To stop Bucardo, simply enter:

    bucardo stop "Reason for stopping"

Again, the reason is optional but recommended.

#### Restarting Bucardo

Restarting is just:

    bucardo restart "Reason for restart"

#### Checking that Bucardo is alive

To send a "ping" to the [MCP](/Bucardo/MCP) process of a running Bucardo, use:

    bucardo ping [timeout]

If successful, an exit value of 0 will be returned. The string returned by this command is Nagios-friendly, and will start with either OK or CRITICAL. The optional timeout argument indicates how long to wait for a response before giving up and returning a critical failure. The default time is 15 seconds. To wait forever, enter a timeout of 0.

### Bucardo configuration

Bucardo stores important configuration variables in the database inside the `bucardo_config` table. See the [Bucardo configuration](/Bucardo/configuration) page for a complete list.

#### Viewing configuration values

To view all of the configuration settings:

    bucardo show all

To view one or more specific items, enter their names:

    bucardo show kick_sleep log_showline

Note that names are actually regular expressions, so that entering:

    bucardo show kid

will list all configuration parameters that have the letters 'kid' inside of them.

#### Changing configuration values

To change a configuration, use:

    bucardo set name=value

For example, to change the syslog logging facility to LOG_LOCAL3:

    bucardo set syslog_facility=LOG_LOCAL3

#### Reloading the configuration settings

To tell a running Bucardo to re-read the configuration table:

    bucardo reload_config

### Controlling syncs

Bucardo works by running one or more replication events called [syncs](/Bucardo/sync). The main interface for controlling these is `bucardo`

#### Kicking a sync

Syncs are fired by changes to the underlying tables, or manually started by [kicking](/Bucardo/cli/kick) them. To kick a sync, use:

    bucardo kick <syncname> [timeout]

The optional timeout argument tells how long `bucardo` will wait for a response from Bucardo indicating that the sync has finished. If no timeout argument is given, the program sends the kick signal and returns immediately. If a value of "0" is given, `bucardo` will wait indefinitely for the sync to finish, and also give a running tab of how long the sync has taken.

Multiple syncs arguments can be given. If not timeout is given, they will all be kicked at once. Otherwise, they will be kicked in the order given, each starting when the previous one has completed. For example, to kick the syncs "sales" and "marketing", while while waiting for each to finish, you could use:

    bucardo kick sales marketing 0

#### Reloading a sync

To reload a sync:

    bucardo reload <syncname>

One or more named syncs can be reloaded this way.  Each will be reloaded
in turn, and `bucardo` will let you know when each has been reloaded.
When a sync is reloaded, the MCP process will stop the existing sync,
reload information about the sync from the database, and start it up again.
This is typically used when you want to make changes to an existing sync
that is already running, e.g. the [onetimecopy](/Bucardo/operations/onetimecopy)
attribute.

#### Activating a sync

To activate a sync that is not currently running, use:

    bucardo activate <syncname>

#### Deactivating a sync

To deactivate a sync that is currently active and running, use:

    bucardo deactivate <syncname>

### Viewing information

To view general status about the currently running Bucardo process, use:

    bucardo status

This will list general information about each sync

#### Detailed sync information

    bucardo status `<syncname>

This will show detailed information about a specific sync, including the last time it successfully ran, the number of rows transferred, and the last time it failed.

#### Listing syncs

To get a list of all [syncs](/Bucardo/sync):

    bucardo list syncs

This list will show the sync name, it's type ([fullcopy](/Bucardo/object_types/fullcopy), [pushdelta](/Bucardo/object_types/pushdelta), or [swap](/Bucardo/object_types/swap)), the source [herd](/Bucardo/object_types/herd), the target database (or database group), and current status. For more details on a specific sync, use the 'status' command above.

#### Listing databases

To get a list of all known databases:

    bucardo list dbs

This will show the name of the database (as used by Bucardo, not its actual name in Postgres), its status, and the connection string used by Bucardo to connect to it.

#### Listing database groups

To get a list of all known [database groups](/Bucardo/object_types/database_group):

    bucardo list dbgroups

#### Listing tables

To list all known tables:

    bucardo list tables

#### Listing sequences

To list all known sequences:

    bucardo list sequences

#### Listing herds

To list all [herds](/Bucardo/object_types/herd):

    bucardo list herds

To list only one or more specific herds, add their names:

    bucardo list herd <herdname>

To get a list of all tables that belong to a herd, use the verbose argument:

    bucardo list herd <herdname> --verbose

### Adding things

To add new items, the general syntax is:

    bucardo add <thing> <name> additional_information

#### Adding a database

Bucardo needs to know how to connect to each database involved in replication. You can teach it about a new database by using:

    bucardo add db <name> [options]

The "name" is the name by which the database will be known to Bucardo,
and must be unique.  This may vary from the actual database name,
as multiple hosts might have databases with the same name.

The other optional arguments are entered in the format name=value and can
include:

-   dbname: the name of the database inside Postgres.  Required unless using
    a service file or setting it via dbdsn.
-   type: The type of the database. Defaults to "postgres". Currently
    supported values are: "postgres", "drizzle", "mongo", "mysql", "maria",
    "oracle", "redis", "sqlite"
-   dbdsn: A direct DSN to connect to a database. Will override all other
    connection options if set.
-   port: the port this database runs on. Defaults to 5432.
-   host: the host this database is on. Defaults to no host (Unix socket)
-   user: the user to connect as. Defaults to 'bucardo'
-   pass: the password to connect with. Don't use this, use a .pgpass file instead!
-   conn: Any additional information add to the connection string, e.g. sslmode=require
-   service: The service name Bucardo should use when connecting to this
    database.
-   status: Initial status of this database. Defaults to "active" but can be
    set to "inactive".
-   dbgroup: Name of the database group this database should belong to.
-   addalltables: Automatically add all tables from this database.
-   addallsequences: Automatically add all sequences from this database.
-   ssp (server_side_prepares): Set to 1 or 0 to enable or disable server-side
    prepares. Defaults to 1.
-   makedelta:  Set to 1 or 0 to enable or disable makedelta. Defaults to 0.

Additional parameters:

-   --force: Forces the database to be added without running a connection test.

For example, to add three new databases on different hosts:

    bucardo add db sales1 dbname=sales host=int-db-sales1
    bucardo add db sales2 dbname=sales host=int-db-sales2
    bucardo add db sales3 dbname=sales host=int-db-sales3

Note: As a convenience, if the "user" value is its default value,
"bucardo", in the event that Bucardo cannot connect to the database, it
will try connecting as "postgres" and create a superuser named
"bucardo".  This is to make things easier for folks getting started with
Bucardo, but will not work if it cannot connect as "postgres", or if it
the connection failed due to an authentication failure.

#### Adding a database group

Databases can be grouped together, so that one master can push to a group
of slave databases rather than a single database.  To create a new named group:

    bucardo add dbgroup name db1:source db2:source db3:target ...

This adds one or more databases to the named dbgroup.  If the dbgroup doesn't
exist, it will be created.  The database parameters should specify their
roles, either "source" or "target".

For example:

    bucardo add dbgroup sales sales1:source sales2:target sales3:target

#### Adding tables

Bucardo needs to know about all tables that might be used in replication. Adding a tables is simply:

    bucardo add table <tablename> db=dbname

The tablename can be schema qualified, but does not have to be. The "dbname" refers to the internal name Bucardo uses to identify databases. The "db=dbname" can be left off if there is only one database in the db table. Note that you only need to add tables from the source database(s).

An easier way to add tables is to simply run:

    bucardo add all tables [db=dbname]

This will not actually change these tables or replicate them, it will merely tell Bucardo about them. Thus, it is safe to run this command at any time.

#### Adding sequences

Bucardo can also replicate sequences that it knows about. To add a sequence:

     bucardo add sequence <seqname> db=dbname

To add all sequences:

     bucardo add all sequences [db=dbname]

All the notes that apply to 'add table' above apply here as well.

#### Adding a herd

A [herd](/Bucardo/object_types/herd) is a named group of tables that are replicated together. To add a herd:

     bucardo add herd <name> [goat goat]

The list of goats are tables or sequences that should be part of this herd.

#### Adding a sync

To add a sync:

     bucardo add sync <name> dbgroup=<dbgroupname> relgroup=<herdname>

The name is simply an internal name used by Bucardo. Keep it short but descriptive: it is used quite often in day to day use. The source is the name of the herd that we are replicating from. The type is one of [fullcopy](/Bucardo/object_types/fullcopy), [pushdelta](/Bucardo/object_types/pushdelta), or [swap](/Bucardo/object_types/swap). The target is either a database (targetdb=<dbname>) or a database group (targetgroup=<groupname>.

As a shortcut for creating new syncs, you can also give a comma-separated list of tables, like so:

     bucardo add sync abc dbgroup=<dbgroupname> tables=sales,marketing,userdb

This will create a herd of the same name as the sync if it does not already exist, add the tables to it, and then create the sync.

Some of the other options that can be added to 'add sync',
in the format name=value:

-   onetimecopy: set the [onetimecopy](/Bucardo/operation/onetimecopy) value for this sync
-   status: set the initial status for the sync. Defaults to 'active'
-   lifetime: set the lifetime for this sync - how long to run before the sync is restarted
-   maxkicks: sets the maxkicks for this sync - how many times it runs before being restarted
-   makedelta: set the [makedelta](/Bucardo/operations/makedelta) value for this sync. Defaults to 0.

### Other actions

#### Sending a message to the log file

To write a custom message to the log file that a current Bucardo process is writing to, use:

    bucardo message "Your message here"

The message will be written by the [MCP](/Bucardo/MCP) process to the logs in the format:

    MESSAGE (date): string

where date is the timestamp the message was added, and string was the message provided

Separate documentation exist for the following commands:

-   [add customname](/Bucardo/cli/add_customname)
-   [add database](/Bucardo/cli/add_database)
-   [add dbgroup](/Bucardo/cli/add_dbgroup)
-   [add herd](/Bucardo/cli/add_herd)
-   [add sync](/Bucardo/cli/add_sync)
-   [add table](/Bucardo/cli/add_table)
-   [kick](/Bucardo/cli/kick)
-   [list customname](/Bucardo/cli/list_customname)
-   [list database](/Bucardo/cli/list_database)
-   [list dbgroup](/Bucardo/cli/list_dbgroup)
-   [list table](/Bucardo/cli/list_table)
-   [remove customname](/Bucardo/cli/remove_customname)
-   [remove database](/Bucardo/cli/remove_database)
-   [remove dbgroup](/Bucardo/cli/remove_dbgroup)
-   [remove sequence](/Bucardo/cli/remove_sequence)
-   [remove table](/Bucardo/cli/remove_table)
-   [update customname](/Bucardo/cli/update_customname)
-   [update database](/Bucardo/cli/update_database)
-   [update dbgroup](/Bucardo/cli/update_dbgroup)
-   [update table](/Bucardo/cli/update_table)
