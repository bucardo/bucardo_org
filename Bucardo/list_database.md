---
title: Bucardo list database
---

The **list database** command is used to list information about one or more databases that Bucardo knows about. It can also be called as **list db**

Example:

bucardo list database`

Shows a list of all databases, one per line, in alphabetical order.

Usage:

` bucardo list database `<name(s)>

If one or more database names is given, only lists the given ones. Wildcards can be used. To view detailed information, use the **--vv** (very verbose) argument. The alternate forms **list databases**, *list db*', and **list dbs** are also accepted.

### Examples

` bucardo list databases`
` `
` Database: main       Type: postgres  Status: active  Conn: psql -p 5432 -U bucardo -d postgres`
` Database: sales      Type: postgres  Status: active  Conn: psql -p 5432 -U bucardo -d sdb`
` Database: m1         Type: mysql     Status: active  Conn: mysql -u bucardo -D sales`
` Database: marketing  Type: postgres  Status: active  Conn: psql -p 5432 -U bucardo -d marketing`

` bucardo list database sales`
` `
` Database: sales      Type: postgres  Status: active  Conn: psql -p 5432 -U bucardo -d sdb`

` bucardo list db ma%`
` `
` Database: main       Type: postgres  Status: active  Conn: psql -p 5432 -U bucardo -d postgres`
` Database: marketing  Type: postgres  Status: active  Conn: psql -p 5432 -U bucardo -d marketing`

` bucardo list database sales -vv`
` `
` Database: sales  Status: active  Conn: psql -p 5432 -U bucardo -d sdb`
`   Belongs to database group fizzy (target)`
`   Used in sync s1 in a role of source`
`     cdate                = 2011-10-10 16:33:02.376544-04`
`     dbconn               = `
`     dbhost               = `
`     dbname               = sales`
`     dbpass               = NULL`
`     dbport               = 5432`
`     dbservice            = NULL`
`     dbtype               = postgres`
`     dbuser               = bucardo`
`     epoch                = 1318278782.37654`
`     makedelta            = 0`
`     name                 = sales`
`     pgpass               = NULL`
`     server_side_prepares = 1`
`     sourcelimit          = 0`
`     status               = active`
`     targetlimit          = 0`

### Internals

Information is read from the [bucardo.db table](/Bucardo/bucardo.db_table) for the main information, from the [bucardo.dbmap table](/Bucardo/bucardo.dbmap_table) for dbgroup memberships, and from the [bucardo.sync table](/Bucardo/bucardo.sync_table) and [bucardo.dbgroup](/Bucardo/bucardo.dbgroup) table for sync information.

### See also:

-   [add_db](/Bucardo/add_db)
-   [update_db](/Bucardo/update_db)
-   [remove_db](/Bucardo/remove_db)
