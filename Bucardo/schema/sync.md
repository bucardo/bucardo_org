---
title: Bucardo tables bucardo.sync
---


<h2>
Table: bucardo.sync

</h2>
<table border="1" cellpadding="3">
<caption style="white-space: nowrap">
<b>Defines a single replication event from a herd to one or more target databases</b>

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
<b>source</b>

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
<b>targetdb</b>

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
<b>targetgroup</b>

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
<b>synctype</b>

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
<b>stayalive</b>

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
<b>kidsalive</b>

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
<b>use[customselect](/Bucardo/operations/customselect)</b>

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
<b>copytype</b>

</td>
<td>
TEXT

</td>
<td>
NOT NULL DEFAULT <b>'copy'</b>

</td>
</tr>
<tr>
<td>
<b>copyextra</b>

</td>
<td>
TEXT

</td>
<td>
NOT NULL DEFAULT <b>''</b>

</td>
</tr>
<tr>
<td>
<b>deletemethod</b>

</td>
<td>
TEXT

</td>
<td>
NOT NULL DEFAULT <b>'delete'</b>

</td>
</tr>
<tr>
<td>
<b>limitdbs</b>

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
<b>ping</b>

</td>
<td>
BOOLEAN

</td>
<td>
NOT NULL DEFAULT <b>true</b>

</td>
</tr>
<tr>
<td>
<b>do_listen</b>

</td>
<td>
BOOLEAN

</td>
<td>
NOT NULL DEFAULT <b>false</b>

</td>
</tr>
<tr>
<td>
<b>checktime</b>

</td>
<td>
INTERVAL

</td>
<td>
NULL

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
<b>source_makedelta</b>

</td>
<td>
[ONOFF](/Bucardo/domains/bucardo.onoff)

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
[ONOFF](/Bucardo/domains/bucardo.onoff)

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
NOT NULL DEFAULT <b>0</b>

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
<b>txnmode</b>

</td>
<td>
TEXT

</td>
<td>
NOT NULL DEFAULT <b>'SERIALIZABLE'</b>

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
<b>overdue</b>

</td>
<td>
INTERVAL

</td>
<td>
NOT NULL DEFAULT <b>'0 seconds'::interval</b>

</td>
</tr>
<tr>
<td>
<b>expired</b>

</td>
<td>
INTERVAL

</td>
<td>
NOT NULL DEFAULT <b>'0 seconds'::interval</b>

</td>
</tr>
<tr>
<td>
<b>track_rates</b>

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
<b>onetimecopy</b>

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
<b>lifetime</b>

</td>
<td>
INTERVAL

</td>
<td>
NULL

</td>
</tr>
<tr>
<td>
<b>maxkicks</b>

</td>
<td>
INTEGER

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
<b>sync_name_pk</b>

</td>
<td>
PRIMARY KEY (name)

</td>
</tr>
<tr>
<td>
<b>sync_source_herd_fk</b>

</td>
<td>
FOREIGN KEY (source) REFERENCES [bucardo.herd](/Bucardo/schema/bucardo.herd)(name) ON UPDATE CASCADE ON DELETE RESTRICT

</td>
</tr>
<tr>
<td>
<b>sync_targetdb_fk</b>

</td>
<td>
FOREIGN KEY ([targetdb](/Bucardo/targetdb)) REFERENCES [bucardo.db](/Bucardo/schema/bucardo.db)(name) ON UPDATE CASCADE ON DELETE RESTRICT

</td>
</tr>
<tr>
<td>
<b>sync_targetgroup_fk</b>

</td>
<td>
FOREIGN KEY ([targetgroup](/Bucardo/targetgroup)) REFERENCES [bucardo.dbgroup](/Bucardo/schema/bucardo.dbgroup)(name) ON UPDATE CASCADE ON DELETE RESTRICT

</td>
</tr>
<tr>
<td>
<b>sync_type</b>

</td>
<td>
CHECK (synctype IN ('[pushdelta](/Bucardo/pushdelta)','[fullcopy](/Bucardo/fullcopy)','[swap](/Bucardo/swap)'))

</td>
</tr>
<tr>
<td>
<b>sync_copytype</b>

</td>
<td>
CHECK (copytype IN ('insert','copy'))

</td>
</tr>
<tr>
<td>
<b>sync_deletemethod</b>

</td>
<td>
CHECK (deletemethod IN ('truncate', 'delete', 'truncate_cascade'))

</td>
</tr>
<tr>
<td>
<b>sync_validtarget</b>

</td>
<td>
CHECK ((([targetdb](/Bucardo/targetdb) IS NULL) AND ([targetgroup](/Bucardo/targetgroup) IS NOT NULL)) OR (([targetdb](/Bucardo/targetdb) IS NOT NULL) AND ([targetgroup](/Bucardo/targetgroup) IS NULL)))

</td>
</tr>
<tr>
<td>
<b>sync_swap_nogroup</b>

</td>
<td>
CHECK (synctype \<\> '[swap](/Bucardo/swap)' OR [targetdb](/Bucardo/targetdb) IS NOT NULL)

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
<b>sync_source_targetdb_type</b>

</td>
<td>
Yes

</td>
<td>
(source, [targetdb](/Bucardo/targetdb), synctype)

</td>
</tr>
<tr>
<td>
<b>sync_source_targetgroup_type</b>

</td>
<td>
Yes

</td>
<td>
(source, [targetgroup](/Bucardo/targetgroup), synctype)

</td>
</tr>
</table>
