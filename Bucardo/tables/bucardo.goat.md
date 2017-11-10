---
title: Bucardo tables bucardo.goat
---

[Category:Bucardo](/Category:Bucardo "wikilink") [Category:Bucardo_Schema](/Category:Bucardo_Schema "wikilink")

<h2>
Table: bucardo.goat

</h2>
<table border="1" cellpadding="3">
<caption style="white-space: nowrap">
<b>Holds information on each table or sequence that may be replicated</b>

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
NOT NULL DEFAULT <b>nextval('goat_id_seq')</b>

</td>
</tr>
<tr>
<td>
<b>db</b>

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
<b>schemaname</b>

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
<b>tablename</b>

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
<b>reltype</b>

</td>
<td>
TEXT

</td>
<td>
NOT NULL DEFAULT <b>'table'</b>

</td>
</tr>
<tr>
<td>
<b>pkey</b>

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
<b>qpkey</b>

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
<b>pkeytype</b>

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
<b>has_delta</b>

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
<b>ping</b>

</td>
<td>
BOOLEAN

</td>
<td>
NULL

</td>
</tr>
<tr>
<td>
<b>customselect</b>

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
<b>source_makedelta</b>

</td>
<td>
[ONOFF](/Bucardo/domains/bucardo.onoff "wikilink")

</td>
<td>
NOT NULL DEFAULT <b>'inherits'</b>

</td>
</tr>
<tr>
<td>
<b>target_makedelta</b>

</td>
<td>
[ONOFF](/Bucardo/domains/bucardo.onoff "wikilink")

</td>
<td>
NOT NULL DEFAULT <b>'inherits'</b>

</td>
</tr>
<tr>
<td>
<b>rebuild_index</b>

</td>
<td>
SMALLINT

</td>
<td>
NULL DEFAULT <b>0</b>

</td>
</tr>
<tr>
<td>
<b>ghost</b>

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
<b>standard_conflict</b>

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
<b>analyze_after_copy</b>

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
<b>strict_checking</b>

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
<b>delta_bypass</b>

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
<b>delta_bypass_min</b>

</td>
<td>
BIGINT

</td>
<td>
NULL

</td>
</tr>
<tr>
<td>
<b>delta_bypass_count</b>

</td>
<td>
BIGINT

</td>
<td>
NULL

</td>
</tr>
<tr>
<td>
<b>delta_bypass_percent</b>

</td>
<td>
SMALLINT

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
<b>goat_id_pk</b>

</td>
<td>
PRIMARY KEY (id)

</td>
</tr>
<tr>
<td>
<b>goat_db_fk</b>

</td>
<td>
FOREIGN KEY (db) REFERENCES [bucardo.db](/Bucardo/tables/bucardo.db "wikilink")(name) ON UPDATE CASCADE ON DELETE RESTRICT

</td>
</tr>
<tr>
<td>
<b>has_schemaname</b>

</td>
<td>
CHECK (length(schemaname) \> 1)

</td>
</tr>
<tr>
<td>
<b>valid_reltype</b>

</td>
<td>
CHECK (reltype IN ('table','sequence'))

</td>
</tr>
<tr>
<td>
<b>custom_needs_pkey</b>

</td>
<td>
CHECK ([customselect](/Bucardo/customselect "wikilink") IS NULL OR length(pkey) \> 1)

</td>
</tr>
<tr>
<td>
<b>pkey_needs_type</b>

</td>
<td>
CHECK (pkey = '' OR pkeytype IS NOT NULL)

</td>
</tr>
<tr>
<td>
<b>standard_conflict</b>

</td>
<td>
CHECK (((reltype \<\> 'table') OR (standard_conflict IS NULL)) OR (standard_conflict IN ('source','target','skip','random','latest','abort')))

</td>
</tr>
<tr>
<td>
<b>standard_conflict_sequence</b>

</td>
<td>
CHECK (((reltype \<\> 'sequence') OR (standard_conflict IS NULL)) OR (standard_conflict IN ('source','target','skip','lowest','highest')))

</td>
</tr>
</table>
