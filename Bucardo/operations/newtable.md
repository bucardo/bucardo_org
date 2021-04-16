---
title: Bucardo newtable
---

Adding a new table to an existing sync in Bucardo
-------------------------------------------------

Adding a new table to an existing [sync](/Bucardo/object_types/sync) is a fairly easy process. This process that Bucardo already knows about the table; if not, just run:

    bucardo add all tables

The next step is:

    bucardo update sync <syncname> add table <table1> <table2> ...

This adds one or more tables to an existing sync, by adding them to
the source [relgroup](/Bucardo/object_types/relgroup) for this sync.
If the tables are already in the sync, no changes are made.

    bucardo validate <syncname>

This tells Bucardo to run the validate_sync() function, which makes any changes needed on the remote databases (such as adding triggers).

    bucardo update sync onetimecopy=2

This instructs the sync to enter [onetimecopy](/Bucardo/operations/onetimecopy) mode. This step is not needed if the sync is [fullcopy](/Bucardo/object_types/fullcopy). The value of 2 means that only empty tables will be copied over. We do this to ensure that all rows in the new table are copied from the source to the target. Once they are all copied, only the differences are copied from that point forward.

Optionally, you can ask Bucardo to defer index processing until the end of the COPY:

    bucardo update sync onetimecopy=2 rebuild_index=1

This modifies the system tables to "turn off" all indexes on the table before it copies the data in, and then runs a REINDEX immediately afterward. For large tables, this can be a significant speedup.

    bucardo reload <syncname>

This lets the Bucardo daemon know that the sync has changed, and to stop it from running, read in the new information from the database, and start it up again.

After that is done, you can tail the log.bucardo file and watch the changes being made. For large tables, you should see it stop for a while on a line that looks like this:

    KID Running on test_target: COPY public.mytable FROM STDIN

Once finished, you can check on the sync's status. Right after the onetimecopy, the number of inserts for the last run will be very high, with no updates or deletes.

    bucardo status <syncname>
