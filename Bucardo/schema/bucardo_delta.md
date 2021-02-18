---
title: Bucardo tables bucardo delta
---


<h2>
Table: bucardo.bucardo_delta

</h2>
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
<b>tablename</b>

</td>
<td>
OID

</td>
<td>
NOT NULL

</td>
</tr>
<tr>
<td>
<b>rowid</b>

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
<b>txntime</b>

</td>
<td>
TIMESTAMPTZ

</td>
<td>
NOT NULL DEFAULT <b>now()</b>

</td>
</tr>
</table>
