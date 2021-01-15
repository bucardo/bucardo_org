---
title: Bucardo tables bucardo.db connlog
---


<h2>
Table: bucardo.db_connlog

</h2>
<table border="1" cellpadding="3">
<caption style="white-space: nowrap">
<b>Tracks connection attempts to each database when its information changes</b>

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
<b>db</b>

</td>
<td>
TEXT

</td>
<td>
NOT NULL

</td>
</tr>
<tr>
<td>
<b>conndate</b>

</td>
<td>
TIMESTAMPTZ

</td>
<td>
NOT NULL DEFAULT <b>now()</b>

</td>
</tr>
<tr>
<td>
<b>connstring</b>

</td>
<td>
TEXT

</td>
<td>
NOT NULL

</td>
</tr>
<tr>
<td>
<b>status</b>

</td>
<td>
TEXT

</td>
<td>
NOT NULL DEFAULT <b>'unknown'</b>

</td>
</tr>
<tr>
<td>
<b>version</b>

</td>
<td>
TEXT

</td>
<td>
NULL

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
<b>db_connlog_dbid_fk</b>

</td>
<td>
FOREIGN KEY (db) REFERENCES [bucardo.db](/Bucardo/schema/bucardo.db)(name) ON UPDATE CASCADE ON DELETE CASCADE

</td>
</tr>
<tr>
<td>
<b>db_connlog_status</b>

</td>
<td>
CHECK (status IN ('unknown', 'good', 'down', 'unreachable'))

</td>
</tr>
</table>
