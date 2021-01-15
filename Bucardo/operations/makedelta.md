---
title: Bucardo makedelta
---

The **makedelta** process is used by Bucardo to add entries to the [bucardo_delta](/Bucardo/schema/bucardo_delta) and [bucardo_track](/Bucardo/schema/bucardo_track) tables as replication is happening. This is needed if the updates made by a sync need to be read at a later time by a different sync. For example, if you had a [pushdelta](/Bucardo/object_types/pushdelta) sync "alpha" replicating rows from database A to database B, and another pushdelta sync replicating rows from database B to database C, you would need to turn on makedelta for sync "alpha", so that the rows copied from A to B are able to be pikced up as changed rows for the B to C sync.

There are four columns that control the use of makedelta:

-   [goat](/Bucardo/schema/goat).target_makedelta. Controls if a specific table should insert makedelta entries on the target. This can be null, in which case the value of whatever sync it is in is used, 0 to not do makedelta, and 1 to always do makedelta.
-   goat.source_makdelta. Same as above, but for the source database. This is only used by [swap](/Bucardo/object_types/swap) syncs.
-   [sync](/Bucardo/schema/sync).target_makedelta. Controls if this sync should insert makedelta entries or not for each of the tables within that sync. If this is set to 1, all tables will have makedelta enabled, regardless of the goat.target_makedelta setting. If this is set to 0, then makedelta will not be enabled (again, the goat.target_makedelta setting is ignored). However, if sync.target_makdelta is set to NULL, then any goats set as target_makedelta will be run as makedelta (and only those goats).
-   sync.source_makedelta. Same as above, but for the source database. This is only used by [swap](/Bucardo/object_types/swap) syncs.

[swap](/Bucardo/object_types/swap) syncs require both source and target makedelta settings, at either the goat or sync level.

The easiest way to enable makedelta is to simply set it as needed at the sync level. In the example above, you would do:

    bucardo update sync alpha target_makedelta=1

However, if you have many syncs using the same tables, it's easiest to leave the sync level as null, and update the tables:

    bucardo update table tab1 target_makedelta=1
