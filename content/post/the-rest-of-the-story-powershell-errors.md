---
title: The rest of the story (PowerShell errors)
date: 2011-07-21T08:00:00-06:00
draft: false
---

So I got a new server given to me to check over. Unlike most folks I like to open up PowerShell to get quick fix on the configuration. I seem to have gotten used to using PowerShell enough now that it takes me about as much time to do it PowerShell as it would in SSMS. So I like hitting the keyboard more than I do clicking the mouse.

It is a Window Server 2008 box and SQL Server 2008 R2 so I know PowerShell is available to me for my perusing.

Open up PowerShell firing off a few commands as such:
```powershell
[System.Reflection.Assembly]::LoadWithPartialName('Microsoft.SqlServer.Smo') | Out-Null
$s = New-Object 'Microsoft.SqlServer.Management.Smo.Server' MyInstance
```
So good so far. I then go to check a few things to find out what the build number is and what the directory path is for the instance.

`$s.Information.version`

This will give you the Major, Minor, Build, and Revision information of that instance. It returns that no issue. However the next command returns nothing:

`$s.Information.RootDirectory`

What this should have given me is the path to the files for that instance on the server. The `\MSSQL10_50.InstanceName\MSSQL\` path. However all it did was send me back to a prompt, without any output or error message. So I decided to just look at all of the information to see if it returned anything.

`$s.Information`

Which that line returns an error that looked like this:

```
format-default : An exception occurred while executing a Transact-SQL statement or batch.
+ CategoryInfo : NotSpecified: (:) [format-default], ExecutionFailureException
+ FullyQualifiedErrorId : Microsoft.SqlServer.Management.Common.ExecutionFailureException,Microsoft...
```

Which did not really help me, but I had an idea it had something to do with my permissions not being setup correctly. So I took that CategoryInfo line and popped it into the mighty <a href="http://en.wikipedia.org/wiki/Oracle_%28The_Matrix%29" target="_blank">Oracle</a> (aka Google). The first link that came up was a blog post from 2009 by Michiel Wories on <a href="http://blogs.msdn.com/b/mwories/archive/2009/06/08/powershell-tips-tricks-getting-more-detailed-error-information-from-powershell.aspx" target="_blank">how to get more detailed error information from PowerShell</a>. Which stemmed from a blog post Allen White (<a href="http://sqlblog.com/blogs/allen_white/default.aspx" target="_blank">b</a>`|`<a href="http://twitter.com/SQLRunr" target="_blank">t</a>) had written on actually how to <a href="http://sqlblog.com/blogs/allen_white/archive/2009/06/08/handling-errors-in-powershell.aspx" target="_blank">handle errors in PowerShell</a>.

Apparently the message outputted to the console does not include all of the error. There is an "InnerException" that has all the meat of the error. To get that you can execute the command below. Now I believe you can only do this if you are working interactively with the console. If you are running a script you would need to check Allen's post to see how you can capture the error itself when your script is executed.

`$error[0] | Format-List InnerException -Force`

From the output of this command I see the rest of the story:
```
An exception occurred while executing a Transact-SQL statement or batch. ---&gt; The EXECUTE permission was denied on the ojbect 'xp_instance_regread', database 'mssqlsystemresource', schema 'sys'.
The EXECUTE permissions was denied...on and on.
```

Each object that should have been returned from executing `$s.Information` shows the `EXECUTE permission denied` message for that object. Which by itself is cool because you see what is happening in the background, and I now know what is being executed to return that information to me.

So now you know how to get to this information when you get an error in PowerShell that just may not give you enough info to go on. I am now off to get my permissions fixed.
