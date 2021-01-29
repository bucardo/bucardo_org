---
title: Bucardo Tutorial
---

This page describes the steps needed to replicate a sample database,
created by the pgbench utility, with Bucardo.  This will demonstrate simply
master to slave behavior.

Install Bucardo
---------------

The first step is to install Bucardo. Detailed instructions can be found on the [installation page](/Bucardo/installation/).

Once you installed, you should now have a global [bucardo](/Bucardo/cli/)
command available.  Test that you can run it and that you are using
the correct version:

    bucardo --version

### Create and populate the database

Bucardo needs a central database. The install option of bucardo will create and install this database for you. All you need to provide is the location of a Postgres instance you want to use, and a valid PID directory. For this example, we'll use the default values of no host, port 5432, and a user named 'Postgres'. We'll use the **/tmp/bucardo** directory as our piddir value.


    mkdir /tmp/bucardo
    bucardo install --piddir=/tmp/bucardo


You will need to enter a "P" to tell it to proceed. If all goes well, you should see a message like this:

    $ bucardo install --piddir=/tmp/bucardo
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
    Enter a number to change it, P to proceed, or Q to quit: p
    Postgres version is: 8.4
    Attempting to create and populate the bucardo database and schema
    Database creation is complete
    Connecting to database 'bucardo' as user 'bucardo'
    Updated configuration setting "piddir"
    Installation is now complete.
    If you see any unexpected errors above, please report them to bucardo-general@bucardo.org
    You should probably check over the configuration variables next, by running:
    bucardo show all
    Change any setting by using: bucardo set foo=bar

That's it! Time to setup our test databases. NOTE: In this example the source/master and target/slave databases reside within a single instance of he Postgres server, and this installation step is normally only required for the source/master node. In the real world where source/master and target/slave are hosted in separate Postgres servers, each slave node will need to have the role 'bucardo' manually created before proceeding to the next step.

Setup the pgbench databases
---------------------------

The **pgbench** utility that comes with Postgres can be used to create some simple test tables in an existing database. Let's create two databases, test1 (the master), and test2 (the slave).

    createdb test1
    createdb test2

Next, we'll install the pgbench files on each.

    pgbench -i test1
    pgbench -i test2

Now that we have some data, let's get Bucardo to replicate it.

Add the databases
-----------------

Bucardo needs to know about each database it needs to talk to.
The [bucardo](/Bucardo/cli/) program does this with the [add database](/Bucardo/cli/add_database)
option.

    bucardo add database test1 dbname=test1
    bucardo add database test2 dbname=test2

Add the tables
--------------

Bucardo also needs to know about any tables that it may be called on to
replicate.  Adding tables by the [add table](/Bucardo/cli/add_table) command
does not actually start replicating them.  In this case, we're going to use
the handy **add all tables** feature.  Tables are grouped together inside of
Bucardo into [herds](/Bucardo/cli/herd), so we'll also place the newly added
tables into a named herd.  Finally, the pgbench_history table has
no primary key or unique index, therefore we cannot replicate it,
so we're going to exclude it from the herd, using the -T switch.

    $ bucardo add all tables db=test1 -T pgbench_history --herd=pgbench --verbose
    New tables:
      public.pgbench_accounts
      public.pgbench_branches
      public.pgbench_tellers
    New tables added: 3
    Already added: 0

Add the syncs
-------------

A [sync](/Bucardo/object_types/sync) is a named replication event.
Each sync has a source herd; we'll go ahead and create a syncs as well.

    $ bucardo add sync benchdelta relgroup=pgbench dbs=test1,test2
    Added sync "benchdelta"

We are ready to kick off Bucardo at this point. Before we do, let's use the **list** options to bucardo to check everything out.

    $ bucardo list herds
    Herd: pgbench Members: public.pgbench_branches, public.pgbench_tellers, public.pgbench_accounts
      Used in syncs: benchdelta

    $ bucardo list syncs
    Sync "benchdelta"  Relgroup "pgbench"   [Active]
      DB group "benchdelta" test1:source test2:target

    $ bucardo list dbs
    Database: test1  Status: active  Conn: psql -p 5432 -U bucardo -d test1
    Database: test2  Status: active  Conn: psql -p 5432 -U bucardo -d test2

    $ bucardo list tables
    1.  Table: public.pgbench_accounts  DB: sales_master  PK: aid (integer)
    2.  Table: public.pgbench_branches  DB: sales_master  PK: bid (integer)
    3.  Table: public.pgbench_tellers   DB: sales_master  PK: tid (integer)

Start Bucardo
-------------

The final step is to fire it up:

    bucardo start

After a few seconds, the prompt will return.  There will be a log file in
the current directory called **log.bucardo** that you can look through.
To disable the logfile and just rely on syslog use the --debugfile=0 argument.
You can also verify that the Bucardo daemons are running by doing a:

    ps -Afw | grep -i Bucardo

Test Replication
----------------

To verify that things are working properly, let's get some baseline counts:

    $ psql -d test1 -At -c 'select count(*) from pgbench_tellers'
    10

    $ psql -d test2 -At -c 'select count(*) from pgbench_tellers'
    10

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

Now let's make changes to that record, and verify that it gets propagated to the slave (test2)

    $ psql -d test1 -c 'update pgbench_tellers set bid=999 where tid = 1'
    UPDATE 1

    $ psql -d test2 -c 'select * from pgbench_tellers where tid = 1'
     tid | bid | tbalance | filler
    -----+-----+----------+--------
       1 | 999 |        0 |

This ends the demonstration. Feel free to play around more. To stop Bucardo when done, just issue:

    bucardo stop

As you experiment, you might also want to look at the syncs in more detail with:

    bucardo status
    bucardo status benchdelta
