---
title: Sync
---

Bucardo replication events happens in **syncs**, which replicate one or more
tables.

To add a new sync, run:

    bucardo add sync name relgroup=xxx dbs=xxx

-   *name* is what you want to name this sync - keep it short and descriptive
-   *relgroup* is the name of a source [relgroup](/Bucardo/object_types/relgroup)
-   *dbs* are the names of databases
-   *dbgroup* is the name of a [database group](/Bucardo/object_types/database_group)
-   (note: only one of dbs or dbgroup is required)
-   *tables* is an optional list of tables that should be immediately added to the new sync. A [relgroup](/Bucardo/object_types/relgroup) with the same name as the sync itself will be automatically created to contain these tables.

To modify an existing sync, run:

    bucardo update sync name=value

Where name is one of the columns of the [sync table](/Bucardo/schema/sync).

To add a database to an existing sync the **update dbgroup** command should be
used (see [update_dbgroup](/Bucardo/cli/update_dbgroup)).
