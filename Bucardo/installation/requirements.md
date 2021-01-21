---
title: Bucardo Requirements
---

Bucardo itself is a Perl daemon that communicates with a master Bucardo database and the databases that are being replicated. The box that it lives on must have:

-   Perl, at least version 5.8.3
-   DBI. at least version 1.51
-   DBD::Pg, at least version 2.0.0
-   Sys::Hostname, at least version 1.11
-   Sys::Syslog, at least version 0.13
-   [DBIx::Safe](/DBIx-Safe/), at least version 1.2.4
-   [boolean](/Bucardo/installation/boolean)

Bucardo requires a database to install the main bucardo schema on. This database must be Postgres version 8.1 or higher, and must have both the languages [PL/pgSQL](https://www.postgresql.org/docs/current/plpgsql-overview.html) and [PL/PerlU](https://www.postgresql.org/docs/current/plperl.html) available. In addition, the install script requires installation as a superuser: creating a new user named 'bucardo' for this purpose is highly recommended.

Databases involved in replication must be Postgres version 8.1 or higher. The language PL/pgSQL must be available as well, unless the database is only used as a target for "fullcopy" syncs, in which case 8.1 is the only requirement.

In addition, the Bucardo daemon requires a Unix-like system. Currently, it has only been tested on Linux variants, but it should work on BSD, Solaris, and other similar systems. Bucardo will not currently work on Windows, but the ability to do so is probably not that difficult to achieve at this point so let us know if you'd like to help with that. However, you can have a Bucardo daemon on a Linux box that replicates Postgres between two Window boxes.

Extra requirements for bucardo-report:

- `CGI`

Extra requirements for developers to build or test Bucardo:

- `Encode::Locale`
- `Pod::Parser`
