---
title: Bucardo tables bucardo.upgrade log
---


<h2>
Table: bucardo.upgrade_log

</h2>
<table border="1" cellpadding="3">
<caption>
<b>Historical record of upgrade actions</b>

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
<b>action</b>

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
<b>summary</b>

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
<b>version</b>

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
