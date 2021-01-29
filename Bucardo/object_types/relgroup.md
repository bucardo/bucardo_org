---
title: Bucardo relgroup
---

A **relgroup** is simply a named group of [tables](/Bucardo/object_types/table). Relgroups are used to designate the "source" of a [sync](/Bucardo/object_types/sync).
Relgroups can be created by running:

    bucardo add relgroup <name> table1 table2 table3...

The list of tables is optional.

Relgroups are stored in the [herd table](/Bucardo/schema/herd). In old versions of Bucardo relgroups were called herds.
