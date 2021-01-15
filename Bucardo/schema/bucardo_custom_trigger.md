---
title: Bucardo tables bucardo.bucardo custom trigger
---


<h2>
Table: bucardo.bucardo_custom_trigger

</h2>
<table border="1" cellpadding="3">
<caption>
<b>Used to override the default bucardo_add_delta trigger on a per-table basis</b>

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
<b>id</b>

</td>
<td>
INTEGER

</td>
<td>
NOT NULL DEFAULT <b>nextval('bucardo_custom_trigger_id_seq')</b>

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
NOT NULL

</td>
</tr>
<tr>
<td>
<b>trigger_name</b>

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
<b>trigger_type</b>

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
<b>trigger_language</b>

</td>
<td>
TEXT

</td>
<td>
NOT NULL DEFAULT <b>'plpgsql'</b>

</td>
</tr>
<tr>
<td>
<b>trigger_body</b>

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
<b>trigger_level</b>

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
NOT NULL DEFAULT <b>'active'</b>

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
<b>bucardo_custom_trigger_id_pk</b>

</td>
<td>
PRIMARY KEY (id)

</td>
</tr>
<tr>
<td>
<b>bucardo_custom_trigger_goat_fk</b>

</td>
<td>
FOREIGN KEY ([goat](/Bucardo/goat)) REFERENCES [bucardo.goat](/Bucardo/schema/bucardo.goat)(id) ON DELETE CASCADE

</td>
</tr>
<tr>
<td>
<b>type_is_delta_or_trigger</b>

</td>
<td>
CHECK (trigger_type IN ('delta', 'triggerkick'))

</td>
</tr>
<tr>
<td>
<b>level_is_row_statement</b>

</td>
<td>
CHECK (trigger_level IN ('ROW', 'STATEMENT'))

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
<b>bucardo_custom_trigger_goat_type_unique</b>

</td>
<td>
Yes

</td>
<td>
([goat](/Bucardo/goat), trigger_type)

</td>
</tr>
</table>
