---
title: Pgsi
---

pgsi
----

**pgsi** is the Postgres System Impact report, a script that analyzes Postgres log files and reports on which queries have the highest overall impact on the server. The impact is computed by looking at not only how long each query takes to complete, but how many times it is run, and the time period between subsequent runs. The report show the queries with the highest system impact, grouped by the type of query (SELECT, UPDATE, etc.)

### Download

The latest version of pgsi, 1.7.1, can be downloaded at:

-   [pgsi-1.7.1.tar.gz](http://bucardo.org/downloads/pgsi-1.7.1.tar.gz)

### Basic Usage

To use pgsi, you must run it against a [Postgres](/Postgres "wikilink") logfile that has full logging enabled. Then run:

` perl pgsi.pl --file=logfile > pgsi.html`

### Postgres Logging Options

Make sure the following options are set in your postgresql.conf, or otherwise enabled for the traffic you want pgsi to analyze:

` log_duration = on`
` log_statement = 'all'`

If you're using the stderr log log destination (the default) you'll also need something like the following line prefix at minimum:

` log_line_prefix = '%t %p '`

However pgsi will support additional information following that on the line. For example remote host (*%h*), user name (*%u*), and database name (*%d*) are often useful for filtering the log before analysis, and can be helpful if you need to manually read or track activity through the log itself.

### Command Line Options

-   --version
    -   Returns the version number
-   --verbose
    -   Increases the level of verbosity
-   --help
    -   Gives some basic help
-   --file=x
    -   The log file to parse. If not given, will read stdin. This can be used more than once to read in multiple files at one time.
-   --format=X
    -   Indicates the format of the output file. Current options are **html** and **mediawiki**
-   --mode=X
    -   Indicates the log file mode. Current options are **pid**, **csv**, **bare**, and **syslog**
-   --color
    -   Adds syntax highlighting to the queries in html format. On by default, can be turned off with --no-color

### Bugs and Feature Requests

Bugs should be reported through [the Github Issues page](https://github.com/bucardo/pgsi/issues). Feature requests are welcome there as well, or send us an email.

### Development

Everyone is encouraged to look over and make improvements to the code. The latest development version can be obtained from [GitHub](http://github.com/bucardo/pgsi) by running:

` git clone git@github.com:bucardo/pgsi.git`

