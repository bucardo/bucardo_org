---
title: Bucardo
---

**Bucardo** is an asynchronous [PostgreSQL](http://www.postgresql.org/) replication system, allowing for both multi-master and multi-slave operations. It was developed at [Backcountry.com](http://www.backcountry.com/) by Jon Jensen and Greg Sabino Mullane of [End Point Corporation](https://www.endpoint.com/), and is now in use at many other organizations. Bucardo is free and open source software released under [the BSD license](/Bucardo/LICENSE).

Obtaining Bucardo
-----------------

The latest version of Bucardo, 5.6.0, can be downloaded here:

-   [Bucardo.tar.gz](http://bucardo.org/downloads/Bucardo-5.6.0.tar.gz)
- signature: [Bucardo.tar.gz.asc](http://bucardo.org/downloads/Bucardo-5.6.0.tar.gz.asc)

Bucardo also requires DBIx::Safe, which can be downloaded here:

-   [DBIx-Safe-1.2.5.tar.gz](http://bucardo.org/downloads/DBIx-Safe-1.2.5.tar.gz)

Documentation
-------------

Online documentation is available for the following parts of Bucardo:

-   [Overview of Bucardo](/Bucardo/Overview): A quick overview of Bucardo, explaining what it is and what it is capable of
-   [Bucardo FAQ (Frequently Asked Questions)](/Bucardo/FAQ): Answers to commonly asked questions about Bucardo
-   [Bucardo installation](/Bucardo/installation/installation): Installation instructions for Bucardo
-   [Bucardo Upgrade](/Bucardo/installation/upgrade): Upgrade instructions for Bucardo
-   [pgbench tutorial](/Bucardo/pgbench_example): An example of how to use Bucardo to replicate a database
-   [bucardo](/Bucardo/bucardo): A script used to control an existing Bucardo installation
-   [DBIx::Safe](/DBIx-Safe/): Helper module needed by Bucardo that provides safe versions of DBI database handles

Community
---------

There are many ways you can help the Bucardo project:

-   Tell us how you are using Bucardo (different platforms, Postgres versions, configurations)
-   Edit this wiki
-   Submit bug reports
-   Fix bugs
-   Write code (including helper programs)

Three Bucardo mailing lists are available:

-   [Bucardo-announce](https://bucardo.org/mailman/listinfo/bucardo-announce): This is a low volume list used for notices of new versions, important bugs, and security warnings. It is highly recommended that anyone using Bucardo subscribe to this list.
-   [Bucardo-general](https://bucardo.org/mailman/listinfo/bucardo-general): Used to discuss any aspect of Bucardo. Bug reports, usage questions, feature requests, and general discussions should be sent to this list.

Bucardo users have real-time chat in the [\#bucardo IRC channel on Freenode](http://webchat.freenode.net/?channels=#bucardo).

We track bugs for Bucardo at [github](https://github.com/bucardo/bucardo/issues/).

Development
-----------

Bucardo development is managed in the [Git](http://git-scm.com/) version control system. Bucardo is composed of two separate projects, each of which can be downloaded for local development as follows:

    git clone git@github.com:bucardo/bucardo.git
    git clone git@github.com:bucardo/dbixsafe.git


See the main [GitHub project](http://github.com/bucardo) for easy patch contribution by the general public.
