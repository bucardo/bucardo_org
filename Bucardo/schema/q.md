---
title: Bucardo tables bucardo.q
---


<h2>
Table: bucardo.q

</h2>
<table border="1" cellpadding="3">
<caption>
<b>A queue of individual replication events</b>

</caption>
<tr>
<th>
Column

</th>
<th>
Type

</th>
<th>
Notes

</th>
</tr>
<tr>
<td>
<b>sync</b>

</td>
<td>
TEXT

</td>
<td>
NULL

</td>
</tr>
<tr>
<td>
<b>sourcedb</b>

</td>
<td>
TEXT

</td>
<td>
NULL

</td>
</tr>
<tr>
<td>
<b>targetdb</b>

</td>
<td>
TEXT

</td>
<td>
NULL

</td>
</tr>
<tr>
<td>
<b>ppid</b>

</td>
<td>
INTEGER

</td>
<td>
NOT NULL

</td>
</tr>
<tr>
<td>
<b>pid</b>

</td>
<td>
INTEGER

</td>
<td>
NULL

</td>
</tr>
<tr>
<td>
<b>synctype</b>

</td>
<td>
TEXT

</td>
<td>
NULL

</td>
</tr>
<tr>
<td>
<b>updates</b>

</td>
<td>
BIGINT

</td>
<td>
NULL

</td>
</tr>
<tr>
<td>
<b>inserts</b>

</td>
<td>
BIGINT

</td>
<td>
NULL

</td>
</tr>
<tr>
<td>
<b>deletes</b>

</td>
<td>
BIGINT

</td>
<td>
NULL

</td>
</tr>
<tr>
<td>
<b>started</b>

</td>
<td>
TIMESTAMPTZ

</td>
<td>
NULL

</td>
</tr>
<tr>
<td>
<b>aborted</b>

</td>
<td>
TIMESTAMPTZ

</td>
<td>
NULL

</td>
</tr>
<tr>
<td>
<b>whydie</b>

</td>
<td>
TEXT

</td>
<td>
NULL

</td>
</tr>
<tr>
<td>
<b>ended</b>

</td>
<td>
TIMESTAMPTZ

</td>
<td>
NULL

</td>
</tr>
<tr>
<td>
<b>cdate</b>

</td>
<td>
TIMESTAMPTZ

</td>
<td>
NOT NULL DEFAULT <b>now()</b>

</td>
</tr>
</table>
<table border="1" cellpadding="3" style="margin-top: 15px">
<tr>
<th>
Constraint

</th>
<th>
Definition

</th>
</tr>
<tr>
<td>
<b>q_sync_fk</b>

</td>
<td>
FOREIGN KEY ([sync](/Bucardo/sync)) REFERENCES [bucardo.sync](/Bucardo/schema/bucardo.sync)(name) ON UPDATE CASCADE ON DELETE SET NULL

</td>
</tr>
<tr>
<td>
<b>q_sdb_fk</b>

</td>
<td>
FOREIGN KEY ([sourcedb](/Bucardo/sourcedb)) REFERENCES [bucardo.db](/Bucardo/schema/bucardo.db)(name) ON UPDATE CASCADE ON DELETE SET NULL

</td>
</tr>
<tr>
<td>
<b>q_tdb_fk</b>

</td>
<td>
FOREIGN KEY ([targetdb](/Bucardo/targetdb)) REFERENCES [bucardo.db](/Bucardo/schema/bucardo.db)(name) ON UPDATE CASCADE ON DELETE SET NULL

</td>
</tr>
</table>
<table border="1" cellpadding="3" style="margin-top: 15px">
<tr>
<th>
Index

</th>
<th>
Unique?

</th>
<th>
Definition

</th>
</tr>
<tr>
<td>
<b>q_unique</b>

</td>
<td>
Yes

</td>
<td>
([sync](/Bucardo/sync),[sourcedb](/Bucardo/sourcedb),[targetdb](/Bucardo/targetdb)) WHERE started IS NULL

</td>
</tr>
<tr>
<td>
<b>q_ppid</b>

</td>
<td>
No

</td>
<td>
(ppid,pid) WHERE ended IS NULL AND aborted IS NULL

</td>
</tr>
<tr>
<td>
<b>q_aborted</b>

</td>
<td>
No

</td>
<td>
([sync](/Bucardo/sync)) WHERE started IS NOT NULL AND aborted IS NOT NULL AND ended IS NULL

</td>
</tr>
<tr>
<td>
<b>q_cleanup</b>

</td>
<td>
No

</td>
<td>
(cdate) WHERE ended IS NOT NULL

</td>
</tr>
<tr>
<td>
<b>q_stathelper</b>

</td>
<td>
No

</td>
<td>
(cdate, [sync](/Bucardo/sync)) WHERE ended IS NOT NULL

</td>
</tr>
</table>
