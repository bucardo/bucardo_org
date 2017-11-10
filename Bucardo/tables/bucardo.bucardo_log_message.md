---
title: Bucardo tables bucardo.bucardo log message
---


<h2>
Table: bucardo.bucardo_log_message

</h2>
<table border="1" cellpadding="3">
<caption>
<b>Helper table for sending messages to the Bucardo logging system</b>

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
<b>msg</b>

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
