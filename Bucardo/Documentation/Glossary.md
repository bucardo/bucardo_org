---
title: Bucardo Documentation Glossary
---

Glossary of Terms
=================

db : A named database with connection information.
dbgroup : A Named group of databases. May contain 0 or more databases.
table : A table to be replicated.
sequences : A sequence to be replicated.
relation : A replicable object, i.e., a table or sequence. Internally known as a "goat" for historical reasons.
relgroup : A group of relations, internally known as a "herd" for historical reasons.
customname : Mapping of an original name to a new one. For example, to replicate from one schema to a differently named one, or even to a different table name.
sync : A named replication event, containing information about what to replicate (e.g., a relgroup) from where to where (dbs and their roles). Also contains lots of other meta information. This is the main unit of replication.
customcol : Allows an override of what columns to replicate - rather than "SELECT \*", you can plug in whatever you want here, including adding things not in the source column list!
customcode : A Perl subroutines that can be run at certain points in the sync process. May handle exceptions, handle conflicts, or just run at certain times with no expectation of functionality (e.g., before we drop triggers).
ping : Generally means a sync-level attribute stating whether or not changes to the tables in the sync will immediately fire off a NOTIFY. Sometimes this is not desired if the tables are very busy (in which case it is usually better to simply have the sync check for activity every X seconds), or the sync only needs to run at very specific times.
MCP : The "Master Control Program" is the main program. It receives requests and forks off controllers (CTL) to handle them. Also may fork vacuum (VAC) processes. Does no other direct sync work on its own. Responsible for communication with the outside world. Reads the bucardo database on startup.
CTL : The "Controller" is in charge of running a single sync (one named replication set). Will create one or more kids (KID) to do the actual work. In charge of corralling the kids and reporting things back to the MCP. May be short-lived or persistent (configurable).
KID : A child program forked off by the CTL in charge of doing the actual work. Usually created with a specific mandate, such as "replicate from A to B for sync X". Only talks to the CTL that created it. Also configurable as to whether it exits after doing its work, or hangs around waiting for another job from the controller.
VAC : An internal vacuum process primarily reponsible for keeping the bucardo_delta_\* tables trimmed. Replaces the cron jobs needed in Bucardo 4.

