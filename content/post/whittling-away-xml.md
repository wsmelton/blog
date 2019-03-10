---
title: Whittling away at XML
date: 2013-10-10T08:00:00-06:00
draft: false
---

XML can be one of those things you come across and say “ah, there has got to be a better way”. It is something I have held off working with in SQL Server. However with things for SQL Server performance (e.g. query plans) and such it is hard to stay away from it, if you are a true DBA. My particular desire to understand it more came about after find the deadlock graphs accessible from the <a href="http://technet.microsoft.com/en-us/library/ff877955.aspx" target="_blank">System Health</a> session in SQL Server 2008 R2. [Side note about the link, Microsoft I found only wrote up an article on it for SQL Server 2012 but it has been there since SQL Server 2008.]

So how do you pull it out? I think ever one is lead to <a href="http://www.sqlservercentral.com/articles/deadlock/65658/" target="_blank">this article</a> on SQLServerCentral, by Jonathan Kehayias (<a href="http://www.sqlskills.com/blogs/jonathan/" target="_blank">blog</a> `|` <a href="http://twitter.com/SQLPoolBoy" target="_blank">twitter</a>). So that is how I normally pull it out.

![](/images/deadlocks_xevents_xml.png)

However that just provides a list of rows with the full XML document in each. Which if you only get a few and you never get them again, you might be alright with this…not so much for me. I wanted more information and a pretty table that parsed it all out. This is where I needed to figure out the XML stuff. I looked around the Internet trying to see if folks had already done this type of script, no luck.

I am actually pretty shocked that I could not find a script already, maybe my Bing-fu or Google-fu is off. Most of my searches pointed me toward parsing the XML graphs from Profiler…not going there.

Well I let this subject die down for a while, put it on the back burner (much like my blogging schedule) until a few days ago. I was perusing through previous PASS Summit Sessions and came upon Kendal Van Dyke’s (<a href="http://www.kendalvandyke.com/" target="_blank">blog</a> `|` <a href="http://twitter.com/SQLDBA" target="_blank">twitter</a>) session on “Working with XML In SQL Server”, <a href="http://softconference.com/pass/sessionDetail.asp?SID=274804" target="_blank">here</a>. [_You will need a login to access this presentation, just go ahead and sign up because it is worth it._]. After watching that a few times it provided a greater understanding of what you can do with XML documents.

That led me to try to find a script that parses through the Profiler deadlock graphs since I understood the XML querying stuff a bit more. I could get one that provided output similar to what I wanted and just whittle it down to what I need. I came across a script by Wayne Sheffield right <a href="http://blog.waynesheffield.com/wayne/code-library/shred-deadlock-graph/" target="_blank">here</a>.

After a bit of work going through it I ended up with the output:

![](/images/deadlocks_xevents.png)

Now the script to get the output can be downloaded here: <a href="https://gist.github.com/wsmelton/43888ac05b7eee5bce65a58ed941881a" target="_blank">SystemHealth_Parsed_DeadlockInfo.sql</a>.
