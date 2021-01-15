---
title: Bucardo tables bucardo.herd
---


<h2>
Table: bucardo.herd

</h2>
<table border="1" cellpadding="3">
<caption>
<b>Named group of tables or sequences from the [goat](/Bucardo/object_types/goat) table: used as the 'source' for syncs</b>

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
<b>name</b>

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
<b>herd_name_pk</b>

</td>
<td>
PRIMARY KEY (name)

</td>
</tr>
</table>
