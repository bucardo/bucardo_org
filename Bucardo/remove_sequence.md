---
title: Bucardo remove sequence
---

__NOTOC__

The **remove sequence** command is used to remove a sequence from the internal Bucardo database.

Usage:

    bucardo remove sequence <name(s)>

Removes one or more sequences: the schema is required.

This will not change any running syncs: to do that, you should run:

    bucardo reload <syncname>

### Internals

Items are removed from the [bucardo.goat table](/bucardo.goat_table "wikilink"). Due to cascading foreign keys, deletion may also remove rows from the [bucardo.herdmap table](/bucardo.herdmap_table "wikilink"), the [bucardo.customname table](/bucardo.customname_table "wikilink"), the [bucardo.customcols table](/bucardo.customcols_table "wikilink"), and the [bucardo.bucardo_custom_trigger table](/bucardo.bucardo_custom_trigger_table "wikilink").

### See also:

-   [add_table](/Bucardo/add_table "wikilink")
-   [list_table](/Bucardo/list_table "wikilink")
-   [update_table](/Bucardo/update_table "wikilink")
