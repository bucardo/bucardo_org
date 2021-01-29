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

Items are removed from the [goat table](/Bucardo/schema/goat).
Due to cascading foreign keys, deletion may also remove rows from
the [herdmap table](/Bucardo/schema/herdmap), the [customname table](/Bucardo/schema/customname),
the [customcols table](/Bucardo/schema/customcols), and the [bucardo_custom_trigger table](/Bucardo/schema/bucardo_custom_trigger).

### See also:

-   [add_table](/Bucardo/cli/add_table)
-   [list_table](/Bucardo/cli/list_table)
-   [update_table](/Bucardo/cli/update_table)
