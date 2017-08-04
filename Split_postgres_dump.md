---
title: Split postgres dump
permalink: /Split_postgres_dump/
---

**split_postgres_dump** is a small Perl script that breaks a --schema-only dump file into pre and post sections. The pre section contains everything needed to import the data, while the post section contains those actions that should be done after the data is loaded, namely the creation of indexes, constraints, and triggers.

The latest version (1.3.3) can be downloaded at:

-   [split_postgres_dump](http://bucardo.org/downloads/split_postgres_dump)
-   [split_postgres_dump.asc](http://bucardo.org/downloads/split_postgres_dump.asc)

Development
-----------

Everyone is encouraged to look over and make improvements to the code. The latest development version can be obtained from [GitHub](https://github.com/bucardo/Split_postgres_dump) by running:

`git clone git@github.com:bucardo/Split_postgres_dump.git`

Bugs can be reported at the [GitHub issues page](https://github.com/bucardo/Split_postgres_dump/issues).
