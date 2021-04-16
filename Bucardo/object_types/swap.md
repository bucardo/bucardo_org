---
title: Swap
---

**swap** is a type of Bucardo [sync](/Bucardo/object_types/sync)
in which changes to tables on two databases are exchanged both ways,
in other words, a replication system where each source is also a target.

With swap syncs, the two databases are referred to as "source" and "target",
but things can flow both ways.

Because tables (and sequences) can be updated on both sides, there needs to be
a way to resolve [conflicts](/Bucardo/operations/conflict_handling).
Each table or sequence used in a swap sync must indicate how to resolve
conflicts, either with standard or custom conflicts.  The standard conflicts
are set with the "standard_conflict" field of the [goat table](/Bucardo/schema/goat),
and must be one of these values:

-   source - the rows on the "source" database always "win" (in a conflict, we copy rows from source to target)
-   target - the rows on the "target" database always win
-   skip - any conflicted rows are simply not replicated. Not recommended for most cases.
-   random - each database has an equal chance of winning each time
-   latest - the row that was most recently changed wins
-   abort - the sync is aborted on a conflict

You can also provide custom conflict handlers to allow you to use business
logic for better conflict resolution.
