---
title: Bucardo add table
---

The **add table** command is used to teach Bucardo about a table.

Example:

    # Adds the table named "sales" to Bucardo.
    bucardo add table sales


Usage:

    bucardo add table <name(s)> [relgroup=relgroup]

Adds one or more tables: the schema is optional: if not given, will add all
tables with that name regardless of schema.  Wildcards can be used as well:
the preferred form is a percent sign (%) as the wildcard.  A relgroup can be
specified as well: all new tables will be added to this relgroup.
The relgroup will be created if it does not already exist.

To add all the tables in the database, run:

    bucardo add all tables

### Internals

New tables cause an insert to the [goat table](/Bucardo/schema/goat).
A new relgroup causes an insert to the [herd table](/Bucardo/schema/herd_table).
Adding a table to a relgroup results in an insert to the [herdmap table](/Bucardo/schema/herdmap).

### See also:

-   [list_table](/Bucardo/cli/list_table)
-   [update_table](/Bucardo/cli/update_table)
-   [remove_table](/Bucardo/cli/remove_table)
