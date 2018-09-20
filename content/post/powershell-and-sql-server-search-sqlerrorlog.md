---
title: Search-SqlErrorLog
date: 2014-12-22T08:00:00-06:00
drafts: false
tags: [powershell, sqlserver]
---

I have had a thought on how I might write this function for some time and finally decided to just sit down and do it.

When you have alerts setup or just in general need to troubleshoot a given instance of SQL Server one of the first steps is always looking through the ERRORLOG files for the instance. You can do this via SSMS or even via T-SQL with a known (but undocumented) stored procedure <a href="http://www.mssqltips.com/sqlservertip/1476/reading-the-sql-server-log-files-using-tsql/" target="_blank">`sp_readerrorlog`</a>. Either of these methods is useful if you are just looking through one log at a time. However, I configure most of the servers I manage to keep at least 15 error logs. I have a few that are set to the max at 99. Trying to search through all of those for one phrase or word can be extremely time consuming to do manually. I guess you could do this with T-SQL, but this is one of those things that PowerShell shines at by allowing more flexibility. I can easily wrap this function into a few lines that will allow me to search for a phrase against multiple servers all at once.

The script is provided below and includes help information so you can use the help cmdlet to pull out the examples or information about each parameter.

```powershell
function Search-SqlErrorLog
{
<#
	.SYNOPSIS
		Allows you to search the error logs of a given SQL Server instance
	.DESCRIPTION
		Utilizes enumeration methods within SMO to iterate through all or some of the error logs on an instance
	.PARAMETER server
		the SQL Server instance
    .PARAMETER logNumber
        number of the specific error log you want to search, or an array of them
    .PARAMETER all
        switch to indicate just search through all error logs of the instance, this is default
	.EXAMPLE
	Search-SqlErrorLog -server MyServer -value "Severity: 25"
	Searches all the logs of an instance for the text "Severity: 25"
	.EXAMPLE
	Search-SqlErrorLog -server MyServer -lognumber 0 -value "Severity: 25"
	Searches through latest error log of an instance for the text "Severity: 25"
    .EXAMPLE
	Search-SqlErrorLog -server MyServer -lognumber 2,5 -value "Severity: 25"
	Searches through two specific error logs for an instance for the text "Severity: 25"
#>

	[CmdletBinding()]
	param (
		[Parameter(Mandatory = $true,Position = 0)]
		[ValidateNotNull()]
		[Alias("instance")]
		[string]$server,

		[Parameter(Mandatory = $false,Position = 1)]
		[AllowNull()]
		[int[]]$lognumber,

		[Parameter(Mandatory = $false,Position = 2)]
		[AllowNull()]
		[switch]$all = $true,

		[Parameter(Mandatory = $true,Position = 3)]
		[ValidateNotNull()]
		[string]$value
	)

	$s = New-Object Microsoft.SqlServer.Management.Smo.Server $server

if ($all)
	{
		$collection = $s.EnumErrorLogs() | select -ExpandProperty name
		for ($i = 1; $i -lt $collection.Count; $i++)
		{
			Write-Progress -Activity "Reading logs" -Status "Reading log number $i" -PercentComplete ($i / $collection.Count * 100)
		}
		foreach ($l in $collection)
		{
			$s.ReadErrorLog($l) | where { $_.Text -match $value } | select @{Label="LogNumber";Expression={$l}}, LogDate, ProcessInfo, Text
		}
	}
	else
	{
		if ($lognumber.Count -eq 1)
		{
			$s.ReadErrorLog($lognumber) | where { $_.Text -match $value } | select LogDate, ProcessInfo, Text
		}
		elseif ($logNumber.Count -gt 0)
		{
			for ($i = 1; $i -lt $logNumber.Count; $i++)
			{
				Write-Progress -Activity "Reading logs" -Status "Reading log number $i" -PercentComplete ($i / $logNumber.Count * 100)
			}
			foreach ($l in $lognumber)
			{
				$s.ReadErrorLog($l) | where { $_.Text -match $value } | select LogDate, ProcessInfo, Text
			}
		}
	}
}
```
