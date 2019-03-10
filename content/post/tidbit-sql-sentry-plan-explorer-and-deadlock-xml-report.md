---
title: SQL Sentry Plan Explorer and Deadlock XML Report
date: 2014-12-15T08:00:00-06:00
drafts: false
tags: [sqlserver]
---

OK, I just found one of those things that I can remember reading about but forgot until I saw it again. Back in October I had the privilege of being the recipient of a SQL Sentry Plan Explorer Pro license via one of their contest:
<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">[Blog] : <a href="https://twitter.com/hashtag/ILovePlanExplorer?src=hash">#ILovePlanExplorer</a> update: <a href="https://twitter.com/wsmelton">@wsmelton</a> won the <a href="https://twitter.com/hashtag/PlanExplorerPRO?src=hash">#PlanExplorerPRO</a> license. Thanks to everyone who participated! <a href="http://t.co/G3jQp62Udx">http://t.co/G3jQp62Udx</a></p>&mdash; SentryOne (@SQLSentry) <a href="https://twitter.com/SQLSentry/status/525330087156404224">October 23, 2014</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

If you are not familar with <a href="http://www.sqlsentry.com" target="_blank">SQL Sentry</a>, you should be. One of the products they are well known for in the SQL Server Community is Plan Explorer. One of the coolest monitoring products they also offer is <a href="http://www.sqlsentry.com/products/performance-advisor/sql-server-performance#prettyPhoto" target="_blank">Performance Advisor</a> that can monitor just about anything you want with your SQL Server environment. One of those features includes the ability to access graphical deadlock analysis. That product includes the ability to export those deadlock graphs similar to the deadlock files you can obtain from SQL Server Profiler. Well one of the many features that exist within the Pro Version of Plan Explorer is the ability to graphically view those deadlock graphs. As some may know one of the more common things you troubleshoot in environments are deadlocks. Being able to easily review those graphs can save a lot of time and headache, if you are a graphical person, which I like pretty pictures.

Well I don't have access to Performance Analzyer for every client I work with (although it would be on the wish list), but I can pull the XML deadlock report from the system_health session in SQL Server 2008 and above. I wondered if I could save that XML data out into a file and open it up in Plan Explorer Pro. So I forced a deadlock to occur on my local instance and pulled it out of the system_health event file. I saved that XML into a file with the XML extension and opened up Plan Explorer...viola:

![](/images/deadlockgraphicalview.png)

How freaking cool!!!
