---
title: Bucardo remove table
---

The **remove table** command is used to remove a table from the internal Bucardo database.

Examples:

    # Removes the table named "sales" in the public schema from Bucardo.
    bucardo remove table public.sales


Database name should be specified if there are two or more tables with same name in different databases.

    # Removes the table named "sales" from the database "bazzo" in the public schema from Bucardo.
    bucardo remove table public.sales db=bazzo

Usage:

    bucardo remove table <name(s)> (db=<dbname>)

Removes one or more tables: the schema is required.

This will not change any running syncs: to do that, you should run:

    bucardo reload <syncname>

### Internals

Items are removed from the [goat table](/Bucardo/schema/goat).
Due to cascading foreign keys, deletion may also remove rows from
the [herdmap table](/Bucardo/schema/herdmap), the [customname table](/Bucardo/schema/customname),
the [customcols table](/Bucardo/schema/customcols), and the [bucardo_custom_trigger table](/Bucardo/schema/bucardo_custom_trigger).

### See also:

-   [add_table](/Bucardo/cli/add_table)
-   [list_table](/Bucardo/cli/list_table)
-   [update_table](/Bucardo/cli/update_table)
