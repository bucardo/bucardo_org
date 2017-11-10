---
title: Bucardo tables bucardo.herdmap
---

[Category:Bucardo](/Category:Bucardo "wikilink") [Category:Bucardo_Schema](/Category:Bucardo_Schema "wikilink")

<h2>
Table: bucardo.herdmap

</h2>
<table border="1" cellpadding="3">
<caption>
<b>Associates a [goat](/Bucardo/goat "wikilink") with one or more herds</b>

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
<b>herd</b>

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
<b>herdmap_herd_fk</b>

</td>
<td>
FOREIGN KEY (herd) REFERENCES [bucardo.herd](/Bucardo/tables/bucardo.herd "wikilink")(name) ON UPDATE CASCADE ON DELETE CASCADE

</td>
</tr>
<tr>
<td>
<b>herdmap_goat_fk</b>

</td>
<td>
FOREIGN KEY ([goat](/Bucardo/goat "wikilink")) REFERENCES [bucardo.goat](/Bucardo/tables/bucardo.goat "wikilink")(id) ON DELETE CASCADE

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
<b>bucardo_herdmap_unique</b>

</td>
<td>
Yes

</td>
<td>
(herd,[goat](/Bucardo/goat "wikilink"))

</td>
</tr>
</table>
