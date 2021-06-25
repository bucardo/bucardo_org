---
title: Bucardo add sync
---

The **add sync** command is used to create a new [Bucardo sync](/Bucardo/object_types/sync).

Example:

    bucardo add sync alpha relgroup=gill dbs=A,B,C

Creates a new sync named **alpha** which replicates tables in
the relgroup **gill** and replicates from source database **A** to
target databases **B** and **C**

Usages:

    bucardo add sync <name> relgroup=<relgroup> dbs=<database group>

    bucardo add sync <name> relgroup=<relgroup> dbs=<list of databases>

    bucardo add sync <name> tables=products,categories,sales dbs=<list of databases>

### Required arguments:

-   relgroup
    -   The [Bucardo relgroup](/Bucardo/object_types/relgroup) containing the tables
        and sequences to be replicated
-   dbs
    -   The [Bucardo database group](/Bucardo/object_types/database_group)
        to use in this sync, or a comma-separated list of databases.
        If the latter, a new database group with the same name as the sync
        will be created.  By default, the first database will be considered
        the [source](/Bucardo/object_types/sourcedb), and all others [targets](/Bucardo/object_types/targetdb).
        To specify the role of a database, add a colon and the role.
        For example, to create a sync with three source databases and two
        targets:

    bucardo add sync foobar relgroup=myrelgroup dbs=A:source,B:target,C:target,D:source,E:source

Because the first database given always defaults to a source role, and all others default to a target role, the above sync could also be created with:

    bucardo add sync foobar relgroup=myrelgroup dbs=A,B,C,D:source,E:source

### Optional arguments:

-   tables
    -   A comma-separated list of tables which should be replicated by this
        sync. A new [relgroup](/Bucardo/object_types/relgroup) will be created with
        the same name as the sync to hold these tables.
-   status
    -   The initial status of this sync. Defaults to "active".  The only other
        choice at the moment is "inactive"
-   rebuild_index
    -   Whether to rebuild indexes after each sync, defaults to off (0)
-   onetimecopy
    -   Controls if we switch to fullcopy mode for normal targets.
        The default is 0 (off).  A setting of 1 indicates a normal onetimecopy.
        A setting of 2 indicates that we only copy if the source table is
        not-empty and the target table is empty.  After a successful sync,
        Bucardo will flip this value back to 0 itself.  See [onetimecopy](/Bucardo/operations/onetimecopy)
        for more information.
-   ping
    -   Determine if triggers are created that signal Bucardo to run when
        a table on one of the source databases for this sync has changes.
        Defaults to 1 (on).
-   autokick
    -   Set whether or not tables in the sync should automatically send
        kick messages when they're modified.  May be overridden by
        the "autokick" parameter of individual tables.  Defaults to 1 (on).
    -   Setting it to 0 (off) ensures that while deltas are logged,
        they will not be copied anywhere until you tell Bucardo to do so.
        This option is useful to log the changes to buy time to prepare your
        new database.


### See also:

-   [list_sync](/Bucardo/cli/list_sync)
-   [update_sync](/Bucardo/cli/update_sync)
-   [remove_sync](/Bucardo/cli/remove_sync)

