---
title: Bucardo table
---

To add a table to Bucardo, run:

` bucardo add table `*`tablename`*

where *tablename* can be of the form **mytable** or **myschema.mytable**.

To add all the tables in the database, run:

` bucardo add all tables`

Note that adding a table simply lets Bucardo know that the table is there, but it will not be replicated until you add it to a [sync](/Bucardo/sync "wikilink")

