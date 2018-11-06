---
title: Bucardo kick
---

A Bucardo **kick** is the action of starting a specific [sync](/sync "wikilink") event. The normal way to kick a sync is through the [bucardo](/bucardo "wikilink") program, like so:

` bucardo kick foobar`

This will kick off the sync named *foobar*. If you give a numeric argument, the command will wait that many seconds for Bucardo to report that the sync has finished. If you give the number **0**, the bucardo command will wait until the sync has finished, no matter how long it takes. It will also give you a running count on the command line of how long the sync has been running.

In addition to specifying syncs by their exact name, users can also include SQL wildcards, as in:

` bucardo kick foo%`

After kicking, you can check the status of a sync by running the [status](/status "wikilink") command:

` bucardo status foobar`

