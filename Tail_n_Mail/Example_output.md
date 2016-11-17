---
title: Tail n Mail Example output
permalink: /Tail_n_Mail/Example_output/
---

This is an example of what an email from the [Tail_n_mail](/Tail_n_mail "wikilink") script might look like.


    Date: Fri Mar 19 09:52:30 2010
    Host: hyperion.example.com
    Unique items: 4
    Total matches: 134
    Matches from [A]  /var/log/apps/2010/hyperion/03/19/05/pgsql-warn.log: 60
    Matches from [B]  /var/log/apps/2010/hyperion/03/19/06/pgsql-warn.log: 8
    Matches from [C]  /var/log/apps/2010/hyperion/03/19/07/pgsql-warn.log: 16
    Matches from [D]  /var/log/apps/2010/hyperion/03/19/08/pgsql-warn.log: 31
    Matches from [E]  /var/log/apps/2010/hyperion/03/19/09/pgsql-warn.log: 19

    [1] From files B to E Count: 102
    First: [B] 2010-03-19T06:18:58-06:00 hyperion postgres[27317]
    Last:  [E] 2010-03-19T09:22:50-06:00 hyperion postgres[12493]
    ERROR: syntax error at end of input at character 47 STATEMENT: select count(*) from sometable where = 34

    [2] From files A to E Count: 30
    First: [A] 2010-03-19T05:10:01-06:00 hyperion postgres[9917]
    Last:  [E] 2010-03-19T09:50:01-06:00 hyperion postgres[30464]
    ERROR: insert or update on table "reindeer" violates foreign key constraint "reindeer_ref_antlers"
    DETAIL: Key (antlers)=(green) is not present in table "antlers". STATEMENT: INSERT INTO reindeer
    (age, gender, antler, notes) VALUES ($1,$2,$3,$4)

    [3] From file B
    2010-03-19T06:10:50-06:00 hyperion postgres[12868]: [31-1] ERROR: invalid input syntax for type
    timestamp: " 00:00:00" STATEMENT: SELECT DISTINCT color FROM antler WHERE creation_date
    BETWEEN ' 00:00:00' AND ' 23:59:59'

    [4] From file D
    2010-03-19T06:10:50-06:00 hyperion postgres[12868]: [33-1] FATAL:  role "nosuchuser" does not exist