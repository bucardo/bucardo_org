---
title: Bucardo add dbgroup
---

The **add dbgroup** command creates a database group and optionally adds one or more databases to it.

Example:

    bucardo add dbgroup horses A B C

Creates a new database group named **horses** and puts the databases **A**, **B**, and **C** inside of it. The default roles are used, so database A in this group will be a source database, and B and C will be targets.

Usages:

    bucardo add dbgroup <name> [optional list of databases]

The list of databases is optional, and can include the type of role as well. By default, the first database given is set to a source role, and the others are set to a target role. The role can be specified by adding a colon and then the role name afterwards. Thus, this command is the same as the example above:

    bucardo add dbgroup horses A:source B:target C:target

You can also add new databases to a group with the add dbgroup command. Databases can only be added this way: they are never removed from the group. For example, to add a new database to the same group with a role of fullcopy, use:

    bucardo add dbgroup horses D:fullcopy

### Internals

New database groups are created with an insert to the [dbgroup table](/Bucardo/schema/dbgroup).
Databases that are added to this group cause an insert to the [dbmap table](/Bucardo/schema/dbmap).

### See also:

-   [list_dbgroup](/Bucardo/cli/list_dbgroup)
-   [update_dbgroup](/Bucardo/cli/update_dbgroup)
-   [remove_dbgroup](/Bucardo/cli/remove_dbgroup)
