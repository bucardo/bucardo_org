---
title: Bucardo tables bucardo config
---


<h2>
Table: bucardo.bucardo_config

</h2>
<table border="1" cellpadding="3">
<caption style="white-space: nowrap">
<b>Contains configuration variables for a specific Bucardo instance</b>

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
<b>setting</b>

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
<b>value</b>

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
<b>about</b>

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
<b>type</b>

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
<b>name</b>

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
<b>valid_config_type</b>

</td>
<td>
CHECK (type IN ('[sync](/Bucardo/sync)','[goat](/Bucardo/object_types/goat)'))

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
<b>bucardo_config_unique</b>

</td>
<td>
Yes

</td>
<td>
(setting) WHERE name IS NULL

</td>
</tr>
<tr>
<td>
<b>bucardo_config_unique_name</b>

</td>
<td>
Yes

</td>
<td>
(setting,name,type) WHERE name IS NOT NULL

</td>
</tr>
</table>
