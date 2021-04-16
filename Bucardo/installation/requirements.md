---
title: Bucardo Requirements
---

Bucardo itself is a Perl daemon that communicates with a Bucardo configuration database and the databases that are being replicated. The server that it runs on must have:

-   Perl, at least version 5.8.3
-   DBI, at least version 1.51
-   [DBIx::Safe](/DBIx-Safe/), at least version 1.2.4
-   DBD::Pg, at least version 2.0.0
-   Pod::Parser, for `bucardo help <subcommand>`
-   Sys::Hostname, at least version 1.11
-   Sys::Syslog, at least version 0.13
-   [boolean](/Bucardo/installation/boolean), only needed for MongoDB

Bucardo requires a database to install the main bucardo schema on. This database must be Postgres version 8.1 or higher, and must have both the languages [PL/pgSQL](https://www.postgresql.org/docs/current/plpgsql-overview.html) and [PL/PerlU](https://www.postgresql.org/docs/current/plperl.html) available. In addition, the install script requires installation as a superuser: creating a new user named 'bucardo' for this purpose is highly recommended.

Databases involved in replication must be Postgres version 8.1 or higher. The language PL/pgSQL must be available as well, unless the database is only used as a target for "fullcopy" syncs, in which case 8.1 is the only requirement.

In addition, the Bucardo daemon requires a Unix-like system. It has primarily been tested on Linux variants and macOS, but it should work on FreeBSD, OpenBSD, NetBSD, Solaris, and other similar systems. Bucardo will not currently work on Windows. However, you can have a Bucardo daemon on a Linux server that replicates between two Windows PostgreSQL servers.

Extra requirements for bucardo-report:

- `CGI`

Extra requirements for developers to build or test Bucardo:

- `Encode::Locale`
