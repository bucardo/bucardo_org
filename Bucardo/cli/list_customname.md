---
title: Bucardo list customname
---

The **list customname** command lists information about one or more Bucardo custom name mappings with their internal IDs.

Example:

    bucardo list customnames

Usage:

    bucardo list customnames [number] [schema.tablename]

Without any arguments, lists all custom names. Arguments can be a number, representing the internal ID (mainly used for removing custom names), or the argument can be a fully qualified table name.

### Examples

    $ bucardo list customnames

    1. Table: public.t1 => foobar
    2. Table: public.sales => qs Sync: alpha

### Internals

Information is read from the [customname table](/Bucardo/schema/customname).

### See also:

-   [add_customname](/Bucardo/cli/add_customname)
-   [remove_customname](/Bucardo/cli/remove_customname)
