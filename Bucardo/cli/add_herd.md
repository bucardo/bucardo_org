---
title: Bucardo add herd
---

The **add herd** command is used to create a new [Bucardo herd](/Bucardo/object_types/herd)
(a named group of tables).

Example:

    bucardo add herd chuck t1 t2

Creates a new herd named **chuck** which contains the tables **t1** and **t2**

Usage:

    bucardo add herd <name> table1 [table2 table3 ...]

Note that herds can also be implicitly created with the [add sync](/Bucardo/cli/add_sync)
command and the [add table](/Bucardo/cli/add_table) command.

### See also:

-   [list_herd](/Bucardo/cli/list_herd)
-   [update_herd](/Bucardo/cli/update_herd)
-   [remove_herd](/Bucardo/cli/remove_herd)

