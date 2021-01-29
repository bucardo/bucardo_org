---
title: Bucardo remove database
---

The **remove database** command removes one or more databases from Bucardo's internal tables.

Example:

    # Removes the database entries "A" and "B"
    bucardo remove database A B`


Usage:

    bucardo remove database <name(s)> <--force>

If there are any tables that Bucardo knows about that reside in this database, or any database groups that this database belongs to, the remove command will fail unless the --force option is given. The alternate form **remove db** is also accepted.

### Internals

Removed databases will cause a delete from the [db table](/Bucardo/schema/db).
Database group mappings will cause deletes from the [dbmap table](/Bucardo/schema/dbmap).
Table removals will cause deletes from the [goat table](/Bucardo/schema/goat).

### See also:

-   [add_database](/Bucardo/cli/add_database)
-   [list_database](/Bucardo/cli/list_database)
-   [update_database](/Bucardo/cli/update_database)
