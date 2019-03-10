---
title: SSMS 2012–Object Reference issue with Maintenance Plans
date: 2014-07-21T08:00:00-06:00
drafts: false
tags: [sqlserver]
---

I am amazed at some of the information you can find on the Internet when searching for an issue. Especially with forum posts that mention your issue (or flat out are the exact same), but do not include any final resolution. The best one I came across was <a href="http://www.sqlteam.com/forums/topic.asp?TOPIC_ID=182869" target="_blank">this one on SQLTeam’s forum site</a>, the post by “prett”, and note that this is posted back in 2013:
<blockquote>The Maintenance Plan is actually built with few services which Microsoft releases such as SSIS and SQL Server Job Agent, hence if you want to schedule the maintenance plan then your server needs to have SSIS in order to build the maintenance plan, and Job Agent in order to run at regular periods.
This error message "Object reference not set to an instance of an object" occurs because of one of the required component was not available on the server.</blockquote>

SQL Server 2005 started out requiring SSIS to be installed for maintenance plans to run, however when <a href="http://technet.microsoft.com/en-us/library/bb283536(v=sql.90).aspx#BKMK_DatabaseEngine" target="_blank">Service Pack 2 was released</a> they removed that requirement. As far as I know after that any release of SQL Server kept that same functionality.

Well I came across this issue on my VMWare View desktop that I utilize for one particular client. I was getting this pretty little box every time I tried to create a new maintenance plan on a newly built SQL Server 2012 Failover Cluster Instance:

![](/images/ssms_object_reference.png)

The version of SSMS I was using:

![](/images/ssms_object_reference2.png)

I thought I would apply Service Pack 2 to try and resolve it and noted during that installation it was showing “SQLExpress”. Which did bring to mind that I had installed SQL Server 2012 Management Studio for Express when it was announced that it was the full version of SSMS now. I confirmed this by going to the “Setup Bootstrap” and checking the Summary files for the previous installations on the desktop. I found this:

![](/images/ssms_object_reference3.png)

So I went to Programs and Features and removed it. I then located the installation media for SQL Server 2012 Standard Edition and installed the Management Tools. Then for good measure applied Service Pack 2 for SQL Server 2012:

![](/images/ssms_object_reference4.png)

Low and behold, that solved my issue. I hope those in the future can find this bit of information useful.