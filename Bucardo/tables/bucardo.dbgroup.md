---
title: Bucardo tables bucardo.dbgroup
---


<h2>
Table: bucardo.dbgroup

</h2>
<table border="1" cellpadding="3">
<caption style="white-space: nowrap">
<b>Named groups of databases: used as '[targetgroup](/Bucardo/targetgroup "wikilink")' for syncs</b>

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
<b>dbgroup_name_pk</b>

</td>
<td>
PRIMARY KEY (name)

</td>
</tr>
<tr>
<td>
<b>dbgroup_name_sane</b>

</td>
<td>
CHECK (name \~ E'\^[a-zA-Z]\\\\w\*\$')

</td>
</tr>
</table>
