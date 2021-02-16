---
title: Bucardo tables customcode
---


<h2>
Table: bucardo.customcode

</h2>
<table border="1" cellpadding="3">
<caption>
<b>Holds Perl subroutines that run via hooks in the replication process</b>

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
NOT NULL DEFAULT <b>nextval('customcode_id_seq')</b>

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
NOT NULL UNIQUE

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
<b>whenrun</b>

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
<b>getdbh</b>

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
<b>getrows</b>

</td>
<td>
BOOLEAN

</td>
<td>
NOT NULL DEFAULT <b>'false'</b>

</td>
</tr>
<tr>
<td>
<b>trigrules</b>

</td>
<td>
BOOLEAN

</td>
<td>
NOT NULL DEFAULT <b>'false'</b>

</td>
</tr>
<tr>
<td>
<b>src_code</b>

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
<b>customcode_id_pk</b>

</td>
<td>
PRIMARY KEY (id)

</td>
</tr>
<tr>
<td>
<b>customcode_whenrun</b>

</td>
<td>
CHECK (whenrun IN ('before_txn', 'before_check_rows', 'before_trigger_drop', 'after_trigger_drop', 'after_table_[sync](/Bucardo/sync)', 'exception', 'conflict', 'before_trigger_enable', 'after_trigger_enable', 'after_txn', 'before_[sync](/Bucardo/sync)', 'after_[sync](/Bucardo/sync)'))

</td>
</tr>
</table>
