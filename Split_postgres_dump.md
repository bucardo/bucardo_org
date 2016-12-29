---
title: Split postgres dump
permalink: /Split_postgres_dump/
redirect_from: "/Split"
---

**split_postgres_dump** is a small Perl script that breaks a --schema-only dump file into pre and post sections. The pre section contains everything needed to import the data, while the post section contains those actions that should be done after the data is loaded, namely the creation of indexes, constraints, and triggers.

The latest version (1.3.3) can be downloaded at:

-   [split_postgres_dump](http://bucardo.org/downloads/split_postgres_dump) TODO
-   [split_postgres_dump.asc](http://bucardo.org/downloads/split_postgres_dump.asc) TODO

Development
-----------

Everyone is encouraged to look over and make improvements to the code. The latest development version can be obtained by running:

`git clone `[`git://bucardo.org/split_postgres_dump.git`](git://bucardo.org/split_postgres_dump.git) TODO

There is also a GitHub mirror for easy patch contribution by the general public.
