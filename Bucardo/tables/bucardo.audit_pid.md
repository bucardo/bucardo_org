---
title: Bucardo tables bucardo.audit pid
---

[Category:Bucardo](/Category:Bucardo "wikilink") [Category:Bucardo_Schema](/Category:Bucardo_Schema "wikilink")

<h2>
Table: bucardo.audit_pid

</h2>
<table border="1" cellpadding="3">
<caption>
<b>Keeps track of current PIDs if audit_pid is on: somewhat deprecated</b>

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
NOT NULL DEFAULT <b>nextval('audit_pid_id_seq')</b>

</td>
</tr>
<tr>
<td>
<b>parentid</b>

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
<b>familyid</b>

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
<b>type</b>

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
<b>sync</b>

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
<b>source</b>

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
<b>target</b>

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
<b>master_backend</b>

</td>
<td>
INTEGER

</td>
<td>
NOT NULL DEFAULT <b>pg_backend_pid()</b>

</td>
</tr>
<tr>
<td>
<b>source_backend</b>

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
<b>target_backend</b>

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
NOT NULL

</td>
</tr>
<tr>
<td>
<b>birthdate</b>

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
<b>killdate</b>

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
<b>birth</b>

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
<b>death</b>

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
<b>audit_pid_id</b>

</td>
<td>
Yes

</td>
<td>
(id)

</td>
</tr>
</table>
