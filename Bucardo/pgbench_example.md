---
title: Bucardo Tutorial
---

This page describes the steps needed to replicate a sample database, created by the pgbench utility, with Bucardo. This will demonstrate simple one-direction source to target replication behavior.

Install the Bucardo software
----------------------------

The first step is to install Bucardo. Detailed instructions can be found on the [installation page](/Bucardo/installation/).

Once you installed, you should now have a global [bucardo](/Bucardo/cli/) command available. Test that you can run it and that you are using the current version:

    $ bucardo --version
    bucardo version 5.6.0

Install the bucardo database
----------------------------

Bucardo needs a central database. The `install` option of bucardo creates and installs this database for you. All you need to provide is the location of a Postgres instance you want to use and a valid PID directory.

For this example, we'll use the default values of no host (localhost UNIX socket), port 5432, database superuser `postgres`, and we'll set `/tmp/bucardo` as our PID directory:

    $ mkdir /tmp/bucardo
    $ bucardo install --piddir=/tmp/bucardo

You should see output like this:

    This will install the bucardo database into an existing Postgres cluster.
    Postgres must have been compiled with Perl support,
    and you must connect as a superuser
    We will create a new superuser named 'bucardo',
    and make it the owner of a new database named 'bucardo'
    Current connection settings:
    1. Host:          <none>
    2. Port:          5432
    3. User:          postgres
    4. PID directory: /tmp/bucardo
    Enter a number to change it, P to proceed, or Q to quit:

Type "p" and press the Enter key to tell it to proceed. If all goes well, you should see:

    Postgres version is: 13
    Attempting to create and populate the bucardo database and schema
    Database creation is complete
    Connecting to database 'bucardo' as user 'bucardo'
    Updated configuration setting "piddir"
    Installation is now complete.
    If you see any unexpected errors above, please report them to bucardo-general@bucardo.org
    You should probably check over the configuration variables next, by running:
    bucardo show all
    Change any setting by using: bucardo set foo=bar

Bucardo is now set up and ready to be told what to replicate.

Note: In this example the source and target databases reside within a single Postgres server instance, and this installation step is normally only required for the source node. In the real world where source and target databases are almost always hosted in separate Postgres servers, each target node will need to have the role 'bucardo' manually created before proceeding to the next step.

Set up the pgbench test databases
---------------------------------

The **pgbench** utility that comes with Postgres can be used to create some simple test tables in a database. Let's create two new databases to use for this: test1 (the source), and test2 (the target).

    $ createdb test1
    $ createdb test2

Next, we'll have pgbench install its sample data in each database:

    $ pgbench -i test1
    $ pgbench -i test2

You may need to specify the path to your specific Postgres version's executable, for example:

    $ /usr/pgsql-13/bin/pgbench -i test1

Now that we have some identical data in two databases, let's get Bucardo to replicate changes we make to the source.

Add the databases
-----------------

First Bucardo needs to know about each database it needs to talk to. The [bucardo](/Bucardo/cli/) program does this with the [add database](/Bucardo/cli/add_database) option:

    $ bucardo add database test1 dbname=test1
    $ bucardo add database test2 dbname=test2

Add the tables
--------------

Bucardo also needs to know about any tables that it may be called on to replicate. (Adding tables by the [add table](/Bucardo/cli/add_table) command does not actually start replicating them.)

In this case, we're going to use the handy **add all tables** feature. Tables are grouped together inside of Bucardo into [relgroups](/Bucardo/object_types/relgroup), so we'll also place the newly added tables into a named relgroup. The pgbench_history table has no primary key or unique index, therefore we cannot replicate it, so let's exclude it from the relgroup by using the -T switch:

    $ bucardo add all tables db=test1 -T pgbench_history --relgroup=pgbench --verbose
    Creating relgroup: pgbench
    Added table public.pgbench_accounts to relgroup pgbench
    Added table public.pgbench_branches to relgroup pgbench
    Added table public.pgbench_tellers to relgroup pgbench
    New tables:
      public.pgbench_accounts
      public.pgbench_branches
      public.pgbench_tellers
    New tables added: 3

Add the syncs
-------------

A [sync](/Bucardo/object_types/sync) is a named replication event. Each sync has a source relgroup. Here's how we create a sync:

    $ bucardo add sync benchdelta relgroup=pgbench dbs=test1,test2
    Added sync "benchdelta"
    Created a new dbgroup named "benchdelta"

Now that everything is set up, let's use the **list** options to bucardo to verify:

    $ bucardo list dbs
    Database: test1    Status: active  Conn: psql -U bucardo -d test1
    Database: test2    Status: active  Conn: psql -U bucardo -d test2

    $ bucardo list dbgroups
    dbgroup: benchdelta   Members: test1:source test2:target

    $ bucardo list relgroups
    Relgroup: pgbench    DB: test1  Members: public.pgbench_accounts, public.pgbench_branches, public.pgbench_tellers
      Used in syncs: benchdelta

    $ bucardo list syncs
    Sync "benchdelta"  Relgroup "pgbench"   [Active]
      DB group "benchdelta" test1:source test2:target

    $ bucardo list tables
    1.  Table: public.pgbench_accounts  DB: test1  PK: aid (integer)
    2.  Table: public.pgbench_branches  DB: test1  PK: bid (integer)
    3.  Table: public.pgbench_tellers   DB: test1  PK: tid (integer)

Start Bucardo
-------------

The final step is to start the Bucardo service:

    $ bucardo start

After a few seconds, the prompt will return. There will be a log file in the current directory called **log.bucardo** that you can look through. To disable this logfile and have Bucardo write logs to syslog, use the `--debugfile=0` argument.

You can also verify that the Bucardo daemons are running by looking for their processes:

    $ ps -Afw | grep Bucardo

Test Replication
----------------

To verify that things are working properly, let's get some baseline counts:

    $ psql -d test1 -At -c 'select count(*) from pgbench_tellers'
    10

    $ psql -d test2 -At -c 'select count(*) from pgbench_tellers'
    10

And let's look at the data from a row that we will modify:

    $ psql -d test1 -c 'select * from pgbench_tellers where tid = 1'
     tid | bid | tbalance | filler
    -----+-----+----------+--------
       1 |   1 |        0 |
    (1 row)

    $ psql -d test2 -c 'select * from pgbench_tellers where tid = 1'
     tid | bid | tbalance | filler
    -----+-----+----------+--------
       1 |   1 |        0 |
    (1 row)

Now let's make changes to that row on the source (test1) and verify that it gets propagated to the target (test2):

    $ psql -d test1 -c 'update pgbench_tellers set bid=999 where tid = 1'
    UPDATE 1

    $ psql -d test2 -c 'select * from pgbench_tellers where tid = 1'
     tid | bid | tbalance | filler
    -----+-----+----------+--------
       1 | 999 |        0 |

Checking Status
---------------

You can look at the syncs in more detail with:

    $ bucardo status
    PID of Bucardo MCP: 397396
     Name         State    Last good    Time    Last I/D    Last bad    Time
    ============+========+============+=======+===========+===========+=======
     benchdelta | Good   | 19:05:59   | 1m 9s | 1/1       | none      |

    $ bucardo status benchdelta
    ======================================================================
    Last good                : Jan 28, 2021 19:05:59 (time to run: 1s)
    Rows deleted/inserted    : 1 / 1
    Sync name                : benchdelta
    Current state            : Good
    Source relgroup/database : pgbench / test1
    Tables in sync           : 3
    Status                   : Active
    Check time               : None
    Overdue time             : 00:00:00
    Expired time             : 00:00:00
    Stayalive/Kidsalive      : Yes / Yes
    Rebuild index            : No
    Autokick                 : Yes
    Onetimecopy              : No
    Post-copy analyze        : Yes
    Last error:              :
    ======================================================================

This ends the demonstration. Feel free to play around more on your own!

Stopping Replication
--------------------

When you're done, stop Bucardo with the command:

    $ bucardo stop
