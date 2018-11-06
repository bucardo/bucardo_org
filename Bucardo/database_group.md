---
title: Database group
---

Databases can be grouped together inside of Bucardo, so that a sync may point to a group of databases (via the "targetgroup" column) rather than to a single database.

To create a new database group, run:

` bucardo add dbgroup `<name>` db1 db2 db3...`

