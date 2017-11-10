---
title: Bucardo tables bucardo.db
---

[Category:Bucardo](/Category:Bucardo "wikilink") [Category:Bucardo_Schema](/Category:Bucardo_Schema "wikilink")

<h2>
Table: bucardo.db

</h2>
<table border="1" cellpadding="3">
<caption style="white-space: nowrap">
<b>Holds information about each database used in replication</b>

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
NOT NULL; this is the name Bucardo will use to refer to this database, <b>not necessarily</b> the database's actual name

</td>
</tr>
<tr>
<td>
<b>dbhost</b>

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
<b>dbport</b>

</td>
<td>
TEXT

</td>
<td>
NOT NULL DEFAULT <b>5432</b>

</td>
</tr>
<tr>
<td>
<b>dbname</b>

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
<b>dbuser</b>

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
<b>dbpass</b>

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
<b>dbconn</b>

</td>
<td>
TEXT

</td>
<td>
NOT NULL DEFAULT <b>''</b>; contains connection parameters, such as "sslmode=require"

</td>
</tr>
<tr>
<td>
<b>dbservice</b>

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
<b>pgpass</b>

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
<b>sourcelimit</b>

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
<b>targetlimit</b>

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
<b>server_side_prepares</b>

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
<b>[makedelta](/Bucardo/makedelta "wikilink")</b>

</td>
<td>
[ONOFF](/Bucardo/domains/bucardo.onoff "wikilink")

</td>
<td>
NOT NULL DEFAULT <b>'off'</b>

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
<b>db_name_pk</b>

</td>
<td>
PRIMARY KEY (name)

</td>
</tr>
<tr>
<td>
<b>db_status</b>

</td>
<td>
CHECK (status IN ('active','inactive'))

</td>
</tr>
<tr>
<td>
<b>db_[makedelta](/Bucardo/makedelta "wikilink")</b>

</td>
<td>
CHECK ([makedelta](/Bucardo/makedelta "wikilink") \<\> 'inherit')

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
<b>db_dsn_unique</b>

</td>
<td>
Yes

</td>
<td>
(dbhost,dbport,dbname,dbuser) WHERE NOT name \~ '\^bctest'

</td>
</tr>
</table>
