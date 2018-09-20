---
title: Parse Deadlock Graph from System_Health session
date: 2015-09-16T07:00:00-06:00
drafts: false
tags: [sqlserver]
---

Way back in October (2014) I published the post: <a href="http://wsmelton.github.io/2013-10-10-xml-glad-that-is-over/" target="_blank">XML, Glad that is over</a> (yeah, I know such a good title). In that post I published a script built from researching how to get the deadlock report out of the Extended Event system_health session. Think of this session like the default trace of SQL Server 2005, but way cooler. Anyway...

It was brought up to me recently on <a href="http://dba.stackexchange.com/a/54812/507" target="_blank">an answer I provided on DBA.StackExchange.com</a>, that I needed a 2014 version. When in fact this is required starting on SQL Server 2012 because the Event XML output changed started in this release. You can find an excellent write-up of this from Jonathan Kehayias <a href="https://www.sqlskills.com/blogs/jonathan/extended-events-changes-in-sql-server-2012/" target="_blank">here</a>.

I <a href="https://github.com/wshawnmelton/Toolbox/blob/master/SystemHealth_Parsed_DeadlockInfo.sql" target="_blank">moved the script to my GitHub repository</a>, and provided an update so it can be run on SQL Server 2012 and higher. The comments now include what has to be changed to make it run on SQL Server 2008.

Enjoy.
