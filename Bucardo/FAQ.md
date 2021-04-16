---
title: Bucardo FAQ
---

Bucardo Frequently Asked Questions
----------------------------------

If you have a question that is not answered here, try checking the main [Bucardo](/Bucardo/) page and see the links and community information there.

### What is Bucardo?

Bucardo is a replication program for two or more Postgres databases. Specifically, it is an asynchronous, multi-source, multi-target (sometimes known as master-master and master-slave or master-standby) table-based replication system. It is written in Perl, and makes extensive use of triggers, PL/PgSQL, and PL/PerlU.

### What are the requirements for use?

See [Requirements](/Bucardo/installation/requirements) documentation.

### Can Bucardo do one-direction master-standby replication?

Absolutely. While Bucardo can do multi-source, multi-target replication, many people use it for replicating changes from one source database to one target only, not the reverse.

### Can Bucardo replicate between more than two databases?

Yes, you can have as many sources and targets as you like.

### Does Bucardo need to run on the database that is being replicated?

The Bucardo program itself can run anywhere, and does not have to be on any of the servers involved in replication. The primary advantage to having it run on the same server is reduced network time. A disadvantage is putting all your eggs in one basket.

### How fast will replication occur?

There is no simple answer to this question, as it depends on how many tables you are replicating in one sync, how fast your network is, how busy your database is, etc. As a general rule of thumb, however, changes make it to the other databases within a matter of one or two seconds.

### Can Bucardo replicate DDL (schema changes)?

No.

### What does "Could not add to q" mean

This message is innocuous. It simply means that Bucardo is getting signaled to sync more quickly than it can complete a sync. That's quite normal, and Bucardo will catch up.

### Will Bucardo work on Windows?

Bucardo will not run natively on Windows, as it has some Unix-specific features. However, the only part of Bucardo that needs to run on a Unix system is the Perl daemon: the Bucardo database and all databases to be replicated can be running on Windows.

It would be nice to get Bucardo working at some point as a native Windows service. Some of the factors that are currently preventing it from running on Windows:

-   Use of fork() and setsid()
-   Heavy use of PIDs
-   Sys::Syslog module

### Does Bucardo support truncate events?

Bucardo supports replication of truncate events when the source database is PostgreSQL version 8.4 or higher. In addition, truncate support is currently only completely working for [pushdelta](/Bucardo/object_types/pushdelta) syncs.
