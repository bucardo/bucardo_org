---
title: Bucardo Failover
---

Failover is possible using Bucardo, although that is not one of its primary goals. For [swap syncs](/Bucardo/swap_syncs), of course, there is very little that needs to be done - just point your application to the other database. For a [pushdelta sync](/Bucardo/pushdelta_sync) on the other hand, making one of the slaves into a master involves the following steps:

-   Set the old master as 'inactive' in the [db table](/Bucardo/db_table).
-   Alter the sync so that the new master is the sourcedb.
-   Run [validate_sync](/Bucardo/validate_sync) so that triggers and other supporting items get created on the new master.
-   If you are in doubt that the slaves are up to date, set [onetimecopy](/Bucardo/operations/onetimecopy) to 2.
-   Restart Bucardo

