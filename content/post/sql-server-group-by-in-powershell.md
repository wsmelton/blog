---
title: SQL Server GROUP BY in PowerShell
date: 2014-11-17T08:00:00-06:00
drafts: false
tags: [powershell,sqlserver]
---

I usually don't have any specific reason to play with PowerShell other than strict joy of doing it, but this time I did. I wanted to go through a client's server, and find out how many tables each database had.

Now something like this can easily be done in T-SQL for a single database with this bit of code:

```sql
SELECT COUNT(*) AS TotalCount
FROM sys.all_objects
WHERE is_ms_shipped = 0 AND type='U'
```

The above works but then you have to write the additional code to execute that against every database on a given server. I prefer to use PowerShell one-liners to get things like this done, at least when I can.

In this instance I figured out how I can by introducing you to the <a href="http://technet.microsoft.com/en-us/library/ee176864.aspx" target="_blank">Group-Object</a> cmdlet. This cmdlet can have a property passed to it and will provide a count based on the number of objects it finds based on that property. So what is done above can easily be accomplished using these two lines (ok isn't a one-liner):

```powershell
Import-Module SQLPS -DisableNameChecking
$s = New-Object Microsoft.SqlServer.Management.Smo.Server ORKO
($s.Databases).Tables | Group-Object Parent | select Count, Name
```

The above will output the below against my local instance of SQL Server 2012:

![](/images/groupobject.png)
