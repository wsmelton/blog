---
title: Max User Connections set to one (oops)
date: 2014-11-11T07:00:00-06:00
drafts: false
tags: [sqlserver,powershell]
---

I frequent <a href="http://dba.stackexchange.com" target="_blank">Database Administrators</a> forum over on Stack Exchange Network, and came across a <a href="http://dba.stackexchange.com/q/81019/507" target="_blank">question</a> that intrigued me enough to play around with the setting noted in the first sentence: <a href="http://msdn.microsoft.com/en-us/library/ms187030.aspx" target="_blank">Maximum number of concurrent connections</a>. What happens when you set this to one, and how do you set it back to default?

_To make a small note the method or process this OP tried to use just to get a database restored was completely the wrong way to go about it. You should not be making changes to server-level configurations without knowing the full affect they can have, especially if you are on a production instance._

Now, if you read the documentation on this setting the main sentence that should grab you:
<blockquote>The <strong>user connections</strong> option specifies the maximum number of simultaneous user connections that are allowed on an instance of SQL Server.</blockquote>
The default value of zero (0) means unlimited, so it goes without warning that if you set this to anything above zero you are limiting how many connections you can have. I would say that setting this to one is equivalent to setting the instance to single-user mode.

I set this to one on my local SQL Server 2012 instance and restarted the instance; because any current connections are not going to be closed automatically by setting this value. Once I tried to connect back to my instance I receive this error:

![](/img/maxconnections_1.png)

Now what do you do to get access again? The most voted answer to the question states try using the DAC to connect. Alright, let us see what happens:

![](/img/maxconnections_2.png)

I will note above is clicking on "New Query" in SSMS, because the initial connection prompt you get when opening SSMS does not support a DAC connection. In doing this it let me connect, but it is not guaranteed in every situation. So what is another method you ask? PowerShell, I answer.

You can make modifications to SQL Server configurations <a href="http://msdn.microsoft.com/en-us/library/ms162157.aspx" target="_blank">using SMO and PowerShell</a>. The example provided actually is what pointed me to these lines of code to fix my predicament:

```powershell
Import-Module SQLPS
$srv = New-Object Microsoft.SqlServer.Management.Smo.Server ORKO
$srv.Configuration.UserConnections.ConfigValue = 1
$srv.Configuration.Alter()
```

Executed the above and restarted the instance and I was back in business. Now I will stipulate that I executed the above code immediately after the instance was restarted so I ensured I grabbed the only connection allowed. If you have other applications or systems that are hitting your instance you may need to just try the DAC. If the DAC is disabled in your environment (some security standards want to see this disabled) then you will need to do a bit more work to grab that single connection.
