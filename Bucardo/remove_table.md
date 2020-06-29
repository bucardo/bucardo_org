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

Items are removed from the [bucardo.goat table](/bucardo.goat_table "wikilink"). Due to cascading foreign keys, deletion may also remove rows from the [bucardo.herdmap table](/bucardo.herdmap_table "wikilink"), the [bucardo.customname table](/bucardo.customname_table "wikilink"), the [bucardo.customcols table](/bucardo.customcols_table "wikilink"), and the [bucardo.bucardo_custom_trigger table](/bucardo.bucardo_custom_trigger_table "wikilink").

### See also:

-   [add_table](/Bucardo/add_table "wikilink")
-   [list_table](/Bucardo/list_table "wikilink")
-   [update_table](/Bucardo/update_table "wikilink")
