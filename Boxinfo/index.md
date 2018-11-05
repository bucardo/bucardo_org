---
title: Boxinfo
permalink: /Boxinfo/
---

**boxinfo** is a Perl script for quickly gathering all sorts of interesting information about a particular computer, which is then put into a HTML or MediaWiki page. It is very handy for being able to see a quick overview of the boxes that you are responsible for. The script has a highly developed [Postgres](/Postgres "wikilink") section. It was developed at End Point Corporation by Greg Sabino Mullane.

### Download

The latest version, 1.4.0, can be downloaded here:

-   [boxinfo.pl](http://bucardo.org/downloads/boxinfo.pl)
-   [boxinfo.pl.asc](http://bucardo.org/downloads/boxinfo.pl.asc)

### Basic Usage

Usage is simply to run:

` perl boxinfo.pl`

It is preferred that the script gets run as the 'root' user, as some of the information can only be gathered by that user. Two files are created by the script:

#### boxinfo.html

This is the final result, either in HTML or MediaWiki format (see the --format argument below). A [sample output page](/Boxinfo/Example "wikilink") is available.

#### boxinfo.debug

This is a copy of each command that was run, and the result. Feel free to delete it, it is only useful for debugging.

### Command Line Options

-   --version
    -   Returns the version number.
-   --verbose
    -   Increases the level of verbosity.
-   --format=X
    -   Which format to output. Valid options are 'html' and 'wiki'. The default is 'wiki', which creates the page with special features to support MediaWiki.
-   --os=X
    -   Overrides automatic detection of the OS with the given name.
-   --client=X
    -   Overrides automatic detection of the client name (derived from the first part of the hostname). This is used at the top of the output, and defaults to 'ACME' if the name cannot be determined.
-   --postgresonly
    -   Only perform the Postgres-specific parts of the program.
-   --nopostgres
    -   Skip the Postgres-specific parts of the program.
-   --skippgport=X
    -   Do not attempt to connect to the Postgres cluster on the given port number.
-   --nohost
    -   Do not attempt host lookups of IPs. May greatly speed up the running of the script.
-   --nomysql
    -   Skip the Mysql-specific parts of the program.
-   --nosendmail
    -   Skip the Sendmail-specific parts of the program.
-   --useballoons=X
    -   Whether or not to use tooltip balloons for MediaWiki output. Takes 0 or 1, defaults to 1.
-   --timeout=X
    -   Sets the maximum time to wait for each command to finish before giving up. The default is 10 seconds.

### Bugs and Feature Requests

Bugs should be reported through [the GitHub issues tracker](http://github.com/bucardo/boxinfo/issues). Feature requests are welcome there as well, or send us an email.

### Development

Everyone is encouraged to look over and make improvements to the code. The latest development version can be obtained by running:

` git clone `[`git://github.com/bucardo/boxinfo.git`](git://github.com/bucardo/boxinfo.git)

### Contributors

-   Greg Sabino Mullane (greg@endpoint.com)
-   David Christensen (david@endpoint.com)
-   Greg Smith (gsmith@gregsmith.com)
-   Robert Treat (rob@xzilla.net)
