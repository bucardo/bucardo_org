---
title: Bucardo list dbgroup
---

The **list dbgroup** command is used to list information about one or more Bucardo database groups.

Example:

    # Shows a list of all database groups, one per line, in alphabetical order.
    bucardo list dbgroup

Usage:

    bucardo list dbgroup <name(s)>

If one or more group names are given, only lists the given ones. Wildcards can be used. To view detailed information, use the `--vv` (very verbose) argument.

### Examples

    $ bucardo list dbgroup

    Database group: alpha  Members: db1:source db2:target
    Database group: beta   Members: db1:source db2:source db3:target

### Internals

Information is read from the [dbgroup table](/Bucardo/schema/dbgroup) and
[dbmap table](/Bucardo/schema/dbmap).

### See also:

-   [add_dbgroup](/Bucardo/cli/add_dbgroup)
-   [update_dbgroup](/Bucardo/cli/update_dbgroup)
-   [remove_dbgroup](/Bucardo/cli/remove_dbgroup)
