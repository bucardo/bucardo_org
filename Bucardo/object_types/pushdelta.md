---
title: Pushdelta
---

**pushdelta** is a type of Bucardo [sync](/Bucardo/object_types/sync)
that involves pushing changed rows from one database (the master) to one or
more slave databases.  It acts very similar to Slony.

For each pushdelta sync, you tell Bucardo which tables and sequences you wish
to replicate, and which databases to push the changes to.

To populate the slave initially, you have two options:

-   Get the sync running to that delta rows are being saved, then copy
    the data to the slave via another method, such as an LVM snapshot,
    or simply a pg_dump.
-   Get the master and slaves running, then set [onetimecopy](/Bucardo/operations/onetimecopy)=2
    for the sync.  This will do a complete COPY of the table from the master
    to the slaves.  Note that this can be set at any time, so if your slaves
    ever get corrupted, out of sync, etc. you can easily restore them
    to the master's version.  The onetimecopy can be set by running:

    bucardo update sync <syncname> onetimecopy=2
    bucardo reload <syncname>
