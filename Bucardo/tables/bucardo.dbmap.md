---
title: Bucardo tables bucardo.dbmap
---


<h2>
Table: bucardo.dbmap

</h2>
<table border="1" cellpadding="3">
<caption style="white-space: nowrap">
<b>Associates a database with one or more groups</b>

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
<b>dbgroup</b>

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
<b>priority</b>

</td>
<td>
SMALLINT

</td>
<td>
NOT NULL DEFAULT <b>0</b>

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
<b>dbmap_db_fk</b>

</td>
<td>
FOREIGN KEY (db) REFERENCES [bucardo.db](/Bucardo/tables/bucardo.db)(name) ON UPDATE CASCADE ON DELETE CASCADE

</td>
</tr>
<tr>
<td>
<b>dbmap_dbgroup_fk</b>

</td>
<td>
FOREIGN KEY (dbgroup) REFERENCES [bucardo.dbgroup](/Bucardo/tables/bucardo.dbgroup)(name) ON UPDATE CASCADE ON DELETE CASCADE

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
<b>dbmap_unique</b>

</td>
<td>
Yes

</td>
<td>
(db,dbgroup)

</td>
</tr>
</table>
