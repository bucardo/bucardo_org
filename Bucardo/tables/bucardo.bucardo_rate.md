---
title: Bucardo tables bucardo.bucardo rate
---

[Category:Bucardo](/Category:Bucardo "wikilink") [Category:Bucardo_Schema](/Category:Bucardo_Schema "wikilink")

<h2>
Table: bucardo.bucardo_rate

</h2>
<table border="1" cellpadding="3">
<caption>
<b>If track_rates is on, measure how fast replication occurs</b>

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
<b>mastercommit</b>

</td>
<td>
TIMESTAMPTZ

</td>
<td>
NOT NULL

</td>
</tr>
<tr>
<td>
<b>slavecommit</b>

</td>
<td>
TIMESTAMPTZ

</td>
<td>
NOT NULL

</td>
</tr>
<tr>
<td>
<b>total</b>

</td>
<td>
INTEGER

</td>
<td>
NOT NULL

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
<b>bucardo_rate_[sync](/Bucardo/sync "wikilink")</b>

</td>
<td>
No

</td>
<td>
([sync](/Bucardo/sync "wikilink"))

</td>
</tr>
</table>
