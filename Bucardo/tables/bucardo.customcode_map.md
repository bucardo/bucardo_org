---
title: Bucardo tables bucardo.customcode map
---


<h2>
Table: bucardo.customcode_map

</h2>
<table border="1" cellpadding="3">
<caption>
<b>Associates a custom code with one or more syncs or goats</b>

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
<b>code</b>

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
<b>goat</b>

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
<b>active</b>

</td>
<td>
BOOLEAN

</td>
<td>
NOT NULL DEFAULT <b>'true'</b>

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
<b>customcode_map_code_fk</b>

</td>
<td>
FOREIGN KEY (code) REFERENCES [bucardo.customcode](/Bucardo/tables/bucardo.customcode)(id) ON DELETE CASCADE

</td>
</tr>
<tr>
<td>
<b>customcode_map_sync_fk</b>

</td>
<td>
FOREIGN KEY ([sync](/Bucardo/sync)) REFERENCES [bucardo.sync](/Bucardo/tables/bucardo.sync)(name) ON UPDATE CASCADE ON DELETE SET NULL

</td>
</tr>
<tr>
<td>
<b>customcode_map_goat_fk</b>

</td>
<td>
FOREIGN KEY ([goat](/Bucardo/goat)) REFERENCES [bucardo.goat](/Bucardo/tables/bucardo.goat)(id) ON DELETE SET NULL

</td>
</tr>
<tr>
<td>
<b>customcode_map_sync[goat](/Bucardo/goat)</b>

</td>
<td>
CHECK ([sync](/Bucardo/sync) IS NULL OR [goat](/Bucardo/goat) IS NULL)

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
<b>customcode_map_unique_[sync](/Bucardo/sync)</b>

</td>
<td>
Yes

</td>
<td>
(code,[sync](/Bucardo/sync)) WHERE [sync](/Bucardo/sync) IS NOT NULL

</td>
</tr>
<tr>
<td>
<b>customcode_map_unique_[goat](/Bucardo/goat)</b>

</td>
<td>
Yes

</td>
<td>
(code,[goat](/Bucardo/goat)) WHERE [goat](/Bucardo/goat) IS NOT NULL

</td>
</tr>
</table>
