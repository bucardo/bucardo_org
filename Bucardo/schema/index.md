---
title: Bucardo schema
---

The main [Bucardo](/Bucardo/) schema is contained in the **bucardo.schema** file. This file is processed when running *bucardo install* to create the Bucardo control database. There are also some tables and functions that are created on the remote databases. All tables and functions are always in the 'bucardo' schema.

Main Bucardo tables
-------------------

-   [bucardo_config](/Bucardo/schema/bucardo_config)
    -   Holds global configuration information: use **bucardo show all** to view
-   [db](/Bucardo/schema/db)
    -   Contains information about each replicated database. Use **bucardo list dbs** to view.
-   [dbgroup](/Bucardo/schema/dbgroup)
    -   Contains the names of database groups. View with **bucardo list dbgroups**'
-   [dbmap](/Bucardo/schema/dbmap)
    -   Maps databases to database groups (many to many)
-   [goat](/Bucardo/schema/goat)
    -   Contains information on specific items to be replicated: tables or sequences. View with **bucardo list goats**
-   [herd](/Bucardo/schema/herd)
    -   A group of goats is a herd: this contains the names of all herds. View with **bucardo list herds**
-   [herdmap](/Bucardo/schema/herdmap)
    -   Maps goats to herds (many to many)
-   [sync](/Bucardo/schema/sync)
    -   A single named replication event. Links a specific source herd to a remote database or database group. View with **bucardo list syncs**
-   [customcode](/Bucardo/schema/customcode)
    -   Perl subroutines that fire at some point in the replication process. Contains code for conflict handling and exception handling. View with **bucardo list codes**
-   [customcode_map](/Bucardo/schema/customcode_map)
    -   Maps customcodes to a specific sync or a goat
-   [upgrade_log](/Bucardo/schema/upgrade_log)
    -   Populated when you run **bucardo upgrade**
-   [bucardo_rate](/Bucardo/schema/bucardo_rate)
    -   Track latency and speed of sync, when the "track_rates" column of a sync is set to true
-   [bucardo_custom_trigger](/Bucardo/schema/bucardo_custom_trigger)
    -   Allows replacement of the standard trigger for replication of only some rows in a table.
-   [bucardo_log_message](/Bucardo/schema/bucardo_log_message)
    -   Used internally for the messaging feature, e.g. **bucardo message Foobar**
-   [q](/Bucardo/schema/q)
    -   Internal table used by Bucardo to coordinate active syncs
-   [audit_pid](/Bucardo/schema/audit_pid)
    -   Lists the PIDs of active processes. No longer on by default.
-   [db_connlog](/Bucardo/schema/db_connlog)
    -   A historical record of connection attempts to remote databases. Rarely used or needed.

Main Bucardo functions
----------------------

-   [bucardo_purge_q_table(interval)](/Bucardo/schema/bucardo_purge_q_table)
-   [validate_goat()](/Bucardo/schema/validate_goat)
-   [validate_sync()](/Bucardo/schema/validate_sync)
-   [validate_all_syncs()](/Bucardo/schema/validate_all_syncs)

Remote Bucardo tables
---------------------

Each database that is used as a source for a [swap](/Bucardo/swap) or [pushdelta](/Bucardo/pushdelta) sync has the following tables installed into the bucardo schema:

-   [bucardo_delta](/Bucardo/schema/bucardo_delta)
    -   Stores which rows have changed for each replicated table
-   [bucardo_track](/Bucardo/schema/bucardo_track)
    -   Stores which rows have been replicated to which remote targets
-   [bucardo_delta_targets](/Bucardo/schema/bucardo_delta_targets)
    -   Maps tables to remote databases
-   [bucardo_sequences](/Bucardo/schema/bucardo_sequences)
    -   Tracks current status of replicated sequences
-   [bucardo_truncate_trigger](/Bucardo/schema/bucardo_truncate_trigger)
    [bucardo_truncate_trigger_log](/Bucardo/schema/bucardo_truncate_trigger_log)
    -   Tracks truncation of replicated tables

Remote Bucardo functions
------------------------

-   [bucardo_purge_delta(interval)](/Bucardo/schema/bucardo_purge_delta)
-   [bucardo_compress_delta()](/Bucardo/schema/bucardo_compress_delta)
-   [bucardo_audit()](/Bucardo/schema/bucardo_audit)
