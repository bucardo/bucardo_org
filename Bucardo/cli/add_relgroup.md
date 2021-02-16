---
title: Bucardo add relgroup
---

The **add relgroup** command is used to create a new [Bucardo relgroup](/Bucardo/object_types/relgroup)
(a named group of tables and sequences).

Example:

    bucardo add relgroup chuck t1 t2

Creates a new relgroup named **chuck** which contains the tables **t1** and **t2**

Usage:

    bucardo add relgroup <name> table1 [table2 table3 ...]

Note that relgroups can also be implicitly created with the [add sync](/Bucardo/cli/add_sync)
command and the [add table](/Bucardo/cli/add_table) command.

### See also:

-   [list_relgroup](/Bucardo/cli/list_relgroup)
-   [update_relgroup](/Bucardo/cli/update_relgroup)
-   [remove_relgroup](/Bucardo/cli/remove_relgroup)
