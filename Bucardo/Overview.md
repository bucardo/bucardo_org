---
title: Bucardo Overview
permalink: /Bucardo/Overview/
---

This page gives a quick overview of what Bucardo is and how it works. Please consult the 
[Bucardo](/Bucardo) page and the rest of the wiki for more details, and be sure and read the [Frequently Asked Questions page](/Bucardo/FAQ).

Bucardo is at its heart a Perl daemon that listens for NOTIFY requests and acts on them, by connecting to remote databases and copying data back and forth. All the specific information that the daemon needs is stored in the main bucardo database, including a list of all the databases involved in the replication and how to reach them, all the tables that are to be replicated, and how each is to be replicated.

The first step in running Bucardo is to add two or more databases to the main bucardo database. Once this is done, information on which tables are to be replicated are added, as well as any groupings of tables. Then the syncs are added. Syncs are named replication actions, copying a specific set of tables from one server to another server or group of servers.

Once Bucardo has been set up, triggers begin storing information about which rows were changed in all the tables of interest. For a swap sync (multi-master), the process goes like this:

1. A change is made to the table and gets recorded in the bucardo_delta table.
2. A notice is sent to the main Bucardo daemon, letting it know that the table has changed.
3. The daemon notifies the controller for that sync and returns to listening.
4. The controller creates a "kid" to handle the replication, or signals an existing one.
5. The kid starts a new transaction and disables triggers and rules on the tables in question.
6. It then gathers a list of which rows have changed since the last replication, and then compares the two to figure out what should be done.
7. If there is a conflict, then either the standard conflict handler, or a custom one, set per table, is run to sort things out.
8. Triggers and rules are re-enabled, and the transaction commits.
9. If the transaction fails, then any custom exception handlers are run.
10. The child signals to the controller that it has finished.
