---
title: Bucardo tables bucardo.herd
---

## Table: bucardo.herd

Named group of tables or sequences from the [goat](/Bucardo/schema/goat) table: used as the 'source' for syncs.

<table border="1" cellpadding="3">
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
