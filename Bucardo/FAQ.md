---
title: Bucardo FAQ
---

Bucardo Frequently Asked Questions
----------------------------------

If you have a question that is not answered here, try checking the main [Bucardo](/Bucardo "wikilink") page and see the links and community information there.

### What is Bucardo?

Bucardo is a replication program for two or more Postgres databases. Specifically, it is an asynchronous, multi-master, master-slave table-based replication system. It is written in Perl, and uses extensive use of triggers, PL/PgSQL, and PL/PerlU.

### What are the requirements for use?

See [Requirements]({% link Bucardo/Installation/Requirements.md %}) documentation.

### Can Bucardo do master/slave replication?

Absolutely. While Bucardo can do master/master replication, many people use it only for master/slave replication (one master database sending changes to one or more slave databases).

### Can Bucardo replicate between more than two masters?

Yes, you can have as many sources (masters) and targets (slaves) as you like.

### Does Bucardo need to run on the database that is being replicated?

The Bucardo program itself can run anywhere, and does not have to be on any of the servers involved in replication. The primary advantage to having it run on the same server is reduced network time. A disadvantage is putting all your eggs in one basket.

### Why does Bucardo give me warnings on startup about mismatched sequences?

This is a consequence of the bucardo user having different search paths on different Postgres servers. This has been fixed in version 4.5.0.

### How fast will replication occur?

There is no simple answer to this question, as it depends on how many tables you are replicating in one sync, how fast your network is, how busy your database is, etc. As a general rule of thumb, however, changes make it to the other databases within a matter of one or two seconds.

### Can Bucardo replicate DDL?

No, Bucardo relies on triggers, and Postgres does not yet provide DDL triggers or triggers on its system tables.

### What does "Could not add to q" mean

This message looks bad, but is in fact innocuous. It simply means that Bucardo is getting signaled to sync more quickly than it can complete a sync. That's quite normal, and Bucardo will catch up.

### Will Bucardo work on Windows?

Bucardo will not work on Windows boxes, as it has some Unix-specific features. However, the only part of Bucardo that needs to run on a non-Windows box is the Perl daemon: the Bucardo database and all databases to be replicated can be running on Windows.

It would be nice to get Bucardo working at some point as a native Windows service. Some of the factors that are currently preventing it from running on Windows:

-   Use of fork() and setsid()
-   Heavy use of PIDs
-   Sys::Syslog module

### Does Bucardo support truncate events?

Bucardo supports replication of truncate events, but only if the source database is version 8.4 or higher. In addition, truncate support is currently only completely working for [pushdelta]({% link Bucardo/pushdelta.md %}) syncs.

