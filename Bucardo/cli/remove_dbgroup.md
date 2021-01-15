---
title: Bucardo remove dbgroup
---

The **remove dbgroup** command removes one or more database groups from Bucardo's internal tables.

Example:

    # Removes the database group named "foo"
    bucardo remove dbgroup foo


Usage:

    bucardo remove dbgroup <name(s)> <--force>

If there are any syncs that are using the database groups to be removed, the command will fail unless the --force option is given.

### Internals

Removed database groups will cause a delete from the [bucardo.dbgroup table](/Bucardo/bucardo.dbgroup_table) and deletes from the [bucardo.dbmap table](/Bucardo/bucardo.dbmap_table). The --force option may cause deletes from the [bucardo.sync table](/Bucardo/bucardo.sync_table).

### See also:

-   [add_dbgroup](/Bucardo/add_dbgroup)
-   [list_dbgroup](/Bucardo/list_dbgroup)
-   [update_dbgroup](/Bucardo/update_dbgroup)
