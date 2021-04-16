---
title: Bucardo pgpass
---

.pgpass files
-------------

Bucardo can read `.pgpass` files to obtain database connection passwords if `trust` authentication is not in use.

The `.pgpass` file to read for a given database is specified by the pgpass field in bucardo's db table. The field should contain the full path and filename of the `.pgpass` files to read. The value can be entered either by editing the db table or using the bucardo command line tool to specify a `pgpass=` option when adding a database.

**File format**

    hostname:port:database:username:password

**Gotchas:**

-   The `.pgpass` file must be readable by the owner of the postmaster (Postgres server) processs.
-   Wildcards within the `.pgpass` file are not processed by bucardo, although they are by Postgres. You must exactly match the hostname, port, database and username you specified when creating your database in Bucardo for the password lookup to succeed.
-   The postmaster process is not allowed by SELinux to read .pgpass files from PL/pgSQL. A symptom of this is permission denied message in syslog. You can add custom SELinux policy, set SELinux to permissive mode, or disable SELinux to allow reading these files to succeed.
