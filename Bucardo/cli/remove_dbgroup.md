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

Removed database groups will cause a delete from the [dbgroup table](/Bucardo/schema/dbgroup)
and deletes from the [dbmap table](/Bucardo/schema/dbmap).  The --force option
may cause deletes from the [sync table](/Bucardo/schema/sync).

### See also:

-   [add_dbgroup](/Bucardo/cli/add_dbgroup)
-   [list_dbgroup](/Bucardo/cli/list_dbgroup)
-   [update_dbgroup](/Bucardo/cli/update_dbgroup)
