---
title: Bucardo Failover
---

Failover is possible using Bucardo, although that is not one of its primary goals.
For [swap syncs](/Bucardo/object_types/swap), of course, there is very little
that needs to be done; just point your application to the other database.
For a [pushdelta sync](/Bucardo/object_types/pushdelta) on the other hand,
making one of the targets into a source involves the following steps:

-   Set the old source as 'inactive' in the [db table](/Bucardo/schema/db).
-   Alter the sync so that the new source is the sourcedb.
-   Run database function validate_sync() so that triggers and other supporting items get created on the new source.
-   If you are in doubt that the targets are up to date, set [onetimecopy](/Bucardo/operations/onetimecopy) to 2.
-   Restart Bucardo.
