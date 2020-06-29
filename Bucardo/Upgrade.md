---
title: Bucardo Upgrade
---

Upgrading Bucardo
-----------------

To upgrade Bucardo, install the new Bucardo file by downloading the [latest version](/Bucardo#Obtaining_Bucardo "wikilink"), and then running:

    perl Makefile.PL
    make
    make install

Then upgrade your existing Bucardo database by running:

    bucardo upgrade

This will modify your existing Bucardo schema as needed. You should also validate all your syncs by running:

    bucardo validate all

