---
title: Bucardo add database
---

The **add database** command is used to teach Bucardo about a database that
will be involved in replication.  It is usually the first step performed
after the [installation](/Bucardo/installation/).

Example:

    bucardo add database A host=example.com dbname=sales

This will creates a new database entry named **A** which resides on
host **example.com** and is named **sales**. Note that "sales" is the actual
database name that Bucardo will connect to, while "A" is how Bucardo refers
to this specific database, for example when calling [add dbgroup](/Bucardo/cli/add_dbgroup).
A connection to the database will be attempted right away:
see the Verification section below.

Usage:

    bucardo add database <name> <dbname=value> [optional arguments]

The alternate form **add db** is also accepted.

### Required arguments:

-   dbname (can also use 'db')
    -   The database to connect to.

### Optional arguments:

-   dbtype (can also use 'type')
    -   The type of database we are connecting to. Defaults to 'postgres'. Other options are drizzle, mongo, mysql, oracle, redis, and sqlite.
-   dbuser (can also use 'username' or 'user')
    -   The username to connect as. Defaults to 'bucardo'.
-   dbpass (can also use 'password')
    -   The password to connect with. Please avoid if possible by using things such as [Postgres' pgpass file](http://www.postgresql.org/docs/current/static/libpq-pgpass.html).
-   dbport (can also use 'port')
    -   The database port to connect to.
-   dbhost (can also use 'host')
    -   The database host to connect to.
-   dbconn (can also use 'conn')
    -   Additional connection parameters. For example, to specify a SID when using an Oracle target:

    bucardo add db foobar type=oracle host=example.com user=scott conn=sid=abc

-   status
    -   Defaults to 'active'; the only other choice is 'inactive'
-   dbgroup
    -   Which internal [database group](/Bucardo/object_types/database_group) to put this database into. Will be created if needed.
-   addalltables
    -   Automatically add all tables inside of this database. For finer control, see [add_table](/Bucardo/cli/add_table)
-   addallsequences
    -   Automatically add all sequences inside of this database
-   server_side_prepares (can also use 'ssp')
    -   For Postgres databases only, determines if we should use server-side prepares. The default is 1 (on). This may need to be 0 if you are using a connection pooler such as PgBouncer which may get confused by usage of server-side prepares.
-   dbservice
    -   For Postgres databases, the "service name" to use

### Verification

Before a new database is added, a simple connection test if performed to make sure everything is working. Thus, you will need to have the database up and running, as well as have installed any extra Perl modules needed to reach the database. The additional Perl modules you need depend on the database type:

-   Postgres: DBD::Pg
-   Drizzle: DBD::Drizzle
-   Mongo: MongoDB
-   Oracle: DBD::Oracle
-   Redis: Redis
-   SQLite: DBD::SQLite

### Internals

New databases cause an insert to the [db table](/Bucardo/schema/db).
A new database group will cause an insert to the [dbgroup table](/Bucardo/schema/dbgroup).
Databases added to that group will cause an insert to the [dbmap table](/Bucardo/schema/dbmap).
Adding tables and sequences will cause inserts to the [goat table](/Bucardo/schema/goat).

### See also:

-   [list_database](/Bucardo/cli/list_database)
-   [update_database](/Bucardo/cli/update_database)
-   [remove_database](/Bucardo/cli/remove_database)
