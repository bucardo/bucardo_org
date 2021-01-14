---
title: Bucardo remove sequence
---

The **remove sequence** command is used to remove a sequence from the internal Bucardo database.

Usage:

    bucardo remove sequence <name(s)>

Removes one or more sequences: the schema is required.

This will not change any running syncs: to do that, you should run:

    bucardo reload <syncname>

### Internals

Items are removed from the [bucardo.goat table](/Bucardo/bucardo.goat_table). Due to cascading foreign keys, deletion may also remove rows from the [bucardo.herdmap table](/Bucardo/bucardo.herdmap_table), the [bucardo.customname table](/Bucardo/bucardo.customname_table), the [bucardo.customcols table](/Bucardo/bucardo.customcols_table), and the [bucardo.bucardo_custom_trigger table](/Bucardo/bucardo.bucardo_custom_trigger_table).

### See also:

-   [add_table](/Bucardo/add_table)
-   [list_table](/Bucardo/list_table)
-   [update_table](/Bucardo/update_table)
