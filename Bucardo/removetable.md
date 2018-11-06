---
title: Bucardo removetable
---

To remove a table or a sequence from an existing sync:

` bucardo update sync `<syncname>` remove table foobar`
` `
` bucardo update sync `<syncname>` remove sequence foobar_seq`

This will not change any running syncs: to do that, you should run:

` bucardo reload `<syncname>

