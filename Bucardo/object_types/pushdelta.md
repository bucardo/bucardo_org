---
title: Pushdelta
---

**pushdelta** is a type of Bucardo [sync](/Bucardo/object_types/sync)
that involves pushing changed rows from one database (the source) to one or
more target databases.

For each pushdelta sync, you tell Bucardo which tables and sequences you wish
to replicate, and which databases to push the changes to.

To populate the target initially, you have two options:

-   Get the sync running to that delta rows are being saved, then copy
    the data to the target via another method, such as an LVM snapshot,
    or simply a pg_dump.
-   Get the source and target databases running, then set [onetimecopy](/Bucardo/operations/onetimecopy)=2
    for the sync. This will do a complete COPY of the table from the source
    to the targets. Note that this can be set at any time, so if your targets
    ever get corrupted, out of sync, etc. you can easily restore them
    to the sources's version. The onetimecopy can be set by running:

    bucardo update sync <syncname> onetimecopy=2
    bucardo reload <syncname>
