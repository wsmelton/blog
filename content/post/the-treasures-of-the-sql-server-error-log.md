---
title: The treasures of the SQL Server Error Log
date: 2014-09-23T08:00:00-06:00
drafts: false
tags: [sqlserver,powershell]
---

I am fairly active on <a href="http://dba.stackexchange.com/users/507/shawn-melton" target="_blank">Database Administrators QA</a> site on <a href="http://stackexchange.com/users/451873/shawn-melton?tab=accounts" target="_blank">StackExchange.com</a>.  On average, most questions you find folks asking are about troubleshooting some error they are getting running code or some application is returning. I have noticed one of the most common comments we end up adding to a question is “have you looked in the error log” or “what error messages show up in the error log”, at least with <a href="http://dba.stackexchange.com/questions/tagged/sql-server" target="_blank">SQL Server related questions</a>.

SQL Server error log is something that every DBA should know how to search and review regularly for the instances in their responsibility. SSMS (GUI) is a common method to look through the error log for an instance, but is only efficient for one instance at a time. Another common method is an undocumented procedure that came around in SQL Server 2005: sp_readerrorlog. I will not go over that one as it is covered pretty well in <a href="http://www.mssqltips.com/sqlservertip/1476/reading-the-sql-server-log-files-using-tsql" target="_blank">this MSSQLTip.com article</a>.

Now I am partial to using PowerShell because it offers a way to perform the same task against one or multiple instances with the a few keystrokes. Now you likely know you don’t necessarily start out with a few keystrokes. I have picked up that if you plan on doing everything more than once, you write it where it only takes you a few keystrokes the next time.

SQL Server Management Objects offer a fairly easy method for pulling the error log for an instance. Creating a new object to an instance and passing it to Get-Member you can see the definition shown:

```powershell
System.Data.DataTable ReadErrorLog(), System.Data.DataTable ReadErrorLog(int logNumber)
```

By default this will return the latest error log for an instance. You can pass in an integer value for older error logs based on how many the instance is configured to keep. Which by default will be 6 (six), so entering a value from 1-6 will give you that particular error log.

```powershell
$srv = New-Object Microsoft.Sqlserver.Management.Smo.Server ORKO\SQL12
$srv.ReadErrorLog()
```

![](/img/read_errorlog.png)

If you do a Get-Member on the method you can see the property values that you can base a filter on: LogDate, ProcessInfo, Text. You can obviously do filtering even easier passing this to Out-GridView, but I will let you play with that on your own.

As an example, say I am reviewing the error log file for possible login issues and I want to return only those failed attempts:

```powershell
$srv = New-Object Microsoft.Sqlserver.Management.Smo.Server ORKO\SQL12
$srv.ReadErrorLog() | where {$_.ProcessInfo -eq "Logon"}
```

![](/img/read_errorlog2.png)

Now if you have an instance configured to log successful and failed login attempts you would want to filter the Text on “failed” to limit the results. As well your error log would obviously be a considerable size on active instances so it can take some time using this method, but it offers a nice break.

Now as I stated previously, writing something the first time so after that it is only a few keystrokes, means you would setup a function to call the code above. I do this with a few extra things added for my purposes, and have it in PowerShell profile so it is available more easily. Below is the current function I use in my profile on a regular basis:

```powershell
function Get-SQLErrorLog ($server,$LogNum,$HowMuch,[switch]$filter)
{
	$srv = New-Object 'Microsoft.SqlServer.Management.Smo.Server' $server
	switch ($LogNum)
	{
		0 { if ($filter)
			{
			# Filter log to exclude:
			#- successful db/log messages
			#- login failed
			#- login succeeded
			#- Information message about runtime of instance (e.g. "This instance of SQL Server has been using process ID...")
			Write-Host "Filtered SQL ERRORLOG on $server" -ForegroundColor Red
			$srv.ReadErrorLog(0) | Where { $_.Text -notmatch 'Login failed' -and $_.Text -notmatch 'Login succeeded ' -and $_.Text -notmatch 'Error: 18456' -and $_.Text -notmatch 'backed up' -and $_.Text -notmatch 'This instance of SQL Server'}
			}
			else
			{
			$srv.ReadErrorLog(0) | Select -Last $HowMuch
			}
		}
		1 {
			if ($filter)
			{
			# Filter log to exclude:
			#- successful db/log messages
			#- login failed
			#- login succeeded
			#- Information message about runtime of instance (e.g. "This instance of SQL Server has been using process ID...")
			Write-Host "Filtered SQL ERRORLOG on $server" -ForegroundColor Red
			$srv.ReadErrorLog(1) | Where { $_.Text -notmatch 'Login failed' -and $_.Text -notmatch 'Login succeeded ' -and $_.Text -notmatch 'Error: 18456' -and $_.Text -notmatch 'backed up' -and $_.Text -notmatch 'This instance of SQL Server'}
			}
			else
			{ $srv.ReadErrorLog(1) | Select -Last $HowMuch }
		}
		2 {
			if ($filter)
			{
			# Filter log to exclude:
			#- successful db/log messages
			#- login failed
			#- login succeeded
			#- Information message about runtime of instance (e.g. "This instance of SQL Server has been using process ID...")
			Write-Host "Filtered SQL ERRORLOG on $server" -ForegroundColor Red
			$srv.ReadErrorLog(2) | Where { $_.Text -notmatch 'Login failed' -and $_.Text -notmatch 'Login succeeded ' -and $_.Text -notmatch 'Error: 18456' -and $_.Text -notmatch 'backed up' -and $_.Text -notmatch 'This instance of SQL Server'}
			}
			else
			{ $srv.ReadErrorLog(2) | Select -Last $HowMuch }
		}
	}
} # End Get-LatestSQLErrorLog
```