---
title: dbatools and a SQL Agent
aliases: [/dbatools-sqlagent/]
date: 2017-08-30T03:30:00-06:00
draft: false
tags: [dbatools]
---

### The mission:

> Tell every DBA around the world about a secret formula that will give them powers.

What power do you think that is? Freedom! Freedom to go work on projects that you want to do versus constantly putting out fires. Freedom to go learn something new.

What is this secret formula? PowerShell and the <a href="https://dbatools.io" target="_blank">dbatools module</a>. This module is meant to make our jobs as a DBA easier and our time managing SQL Server environments more efficient. There are a plethora (no not the <a href="https://youtu.be/OebItXu-QCk" target="_blank">music group</a>) of commands in this module.

You can use `Find-DbaCommand` to explore all the commands in the module, this will let you search an index of the commands via pattern. So if you wanted to find all the commands around disk:

![](/img/dbatools-agent_finddbacommand.png)

### Running via SQL Server Agent

One main thing I have seen folks post about in forums and ask questions about on Slack or Twitter is how to utilize the module via an Agent step. This is possible but at this time can only be done in a particular manner.

You have two options for running PowerShell code via an Agent step.

1. PowerShell
2. Operating System (CmdExec)

#### PowerShell Step

The bad news, at least at the time of this post, is that the PowerShell step cannot be used to run dbatools safely. This step type in Agent does not put you in the same PowerShell host as if you are just running `PowerShell.exe`. You are placed in the `sqlps.exe` host and the SQLSERVER provider. In that environment, it varies based on what version of SQL Server you run, but the main thing is the dbatools module does not interact well with the module for SQL Server. We have some custom types and format files that tend to conflict with the modules for SQL Server.

One other thing I've come across is that importing the module into the sqlps host won't actually work because of the tab completion that is now part of the module (TEPP). You will get an error similar to this when you try to import the module via a PowerShell step in Agent:

> Executed as user: NT Service\SQLSERVERAGENT. A job step received an error at line 109 in a PowerShell script. The corresponding line is '$ExecutionContext.InvokeCommand.InvokeScript($false, ([scriptblock]::Create([io.file]::ReadAllText("$PSScriptRoot\internal\scripts\insertTepp.ps1"))), $null, $null)  '. Correct the script and reschedule the job. The error information returned by PowerShell is: 'Exception calling "InvokeScript" with "4" argument(s): "The module 'TabExpansionPlusPlus' could not be loaded. For more information, run 'Import-Module TabExpansionPlusPlus'."  '.  Process Exit Code -1.  The step failed.

#### Operating System Step

The good news is you can use the CmdExec step and call `PowerShell.exe` with your code passed in or reference a file to run it successfully. Now one caveat to using dbatools module at all is ensuring either the Agent service account has the proper access to the target servers. It will depend on what command(s) you want to use as to what exact access is required. The commands for example that access Windows level information would need local administrator rights for some parts and PowerShell remoting. Where the commands that are simply going to perform an action or get information from a SQL Server, simply need login access to that instance.

An alternative, and the recommended practice, to granting all those rights to the Agent service account is to simply configure a proxy account for the CmdExec subsystem. You can then just grant that account access to the target servers. You can find out how to create a proxy account in the <a href="https://docs.microsoft.com/en-us/sql/ssms/agent/create-a-sql-server-agent-proxy" target="_blank">documentation for SQL Server</a>.

### A Sample Job

As a small example let's say we have the following requirements:

1. Capture space usage for each database on a given instance of SQL Server
2. Include the system databases
3. Collect this information to a table in a database that will have a SSRS or PowerBI report pointed at it for visibility.

#### Capture space usage

So using the `Find-DbaCommand` in the screenshot above we found we can use `Get-DbaDatabaseSpace` to get the space usage for each database. Checking the help content of the file I found it includes a parameter `-IncludeSystem` that will let me include the system database information as well.

![](/img/dbatools-agent_getdbadatabasespace.png)

#### Collect it into a table

Using that find command again, using "table" as the search term, I found `Out-DbaDataTable` and `Write-DbaDataTable` that:

1. Take the output from Get-DbaDatabaseSpace and convert it to a data table.
2. Then take that data table and dump it into a table.

Checking the help for `Write-DbaDataTable`, I will use the `-AutoCreateTable` parameter to have it create the table if it does not already exist. The cool part of this one: if the table already exists it will simply append the data to that table for me.

<iframe src="https://giphy.com/embed/ujUdrdpX7Ok5W" width="280" height="240" frameBorder="0" class="giphy-embed" allowFullScreen></iframe>

However, there is one thing we need to add to the output as it does not do much good to gather this information over each hour, day or month unless we can see when it was captured. We just need to add an additional property to the output of `Get-DbaDatabaseSpace` that will be the timestamp. That is simple enough by using a hash table with the Label (L) and Expression (E) keys. _You can also use "Name" instead of "Label", either one works._

My command to perform a full capture of my local 2016 instance will look like this, which will run via the PowerShell host:

```powershell
# added line breaks for readability
Import-Module dbatools;
$server = 'manatarms'
Get-DbaDatabaseSpace -SqlInstance $server -IncludeSystemDBs |
	Select-Object *, @{L='CaptureDate';E={Get-Date -Format g}} |
	Out-DbaDataTable |
	Write-DbaDataTable -SqlInstance $server -Database db1 -Table FreeSpace -AutoCreateTable
```

I'm just writing my data out to the table "db1.dbo.FreeSpace". If you have more than one server you need to capture to, just add them as a comma-separated list to the `$server` variable.

#### Create the Agent Job

To add this to a job step we simply need to make it all one line and format it with a few more single ticks and double-quotes. The following shows the T-SQL that will create the Agent Job, with no schedule attached, that I can run to capture the data.

```sql
USE [msdb]
GO

DECLARE @ReturnCode INT
SELECT @ReturnCode = 0

DECLARE @jobId BINARY(16)
EXEC @ReturnCode =  msdb.dbo.sp_add_job @job_name=N'dbatools_example',
		@enabled=1,
		@notify_level_eventlog=0,
		@notify_level_email=0,
		@notify_level_netsend=0,
		@notify_level_page=0,
		@delete_level=0,
		@description=N'No description available.',
		@category_name=N'[Uncategorized (Local)]',
		@owner_login_name=N'sa', @job_id = @jobId OUTPUT
EXEC @ReturnCode = msdb.dbo.sp_add_jobstep @job_id=@jobId, @step_name=N'dbatools_command',
		@step_id=1,
		@cmdexec_success_code=0,
		@on_success_action=1,
		@on_success_step_id=0,
		@on_fail_action=2,
		@on_fail_step_id=0,
		@retry_attempts=0,
		@retry_interval=0,
		@os_run_priority=0, @subsystem=N'CmdExec',
		@command=N'powershell.exe -ExecutionPolicy Bypass -Command "Import-Module dbatools; $server = ''manatarms''; Get-DbaDatabaseSpace -SqlInstance $server -IncludeSystemDBs | Select-Object *, @{L=''CaptureDate'';E={Get-Date -Format g}} | Out-DbaDataTable | Write-DbaDataTable -SqlInstance $server -Database db1 -Table FreeSpace -AutoCreateTable',
		@flags=0
EXEC @ReturnCode = msdb.dbo.sp_update_job @job_id = @jobId, @start_step_id = 1
EXEC @ReturnCode = msdb.dbo.sp_add_jobserver @job_id = @jobId, @server_name = N'(local)'
GO
```

![](/img/dbatools-agent_captureddata.png)

##### Use a File

If you desire to use a file instead of inline code you just replace that `@command` with this call to PowerShell:

```sql
@command=N'powershell.exe -ExecutionPolicy Bypass -File D:\ScriptRepo\GetDatabaseSpace.ps1
```

All the code that was previously called is simply put into that file. It is easier to read in the Agent job but does require that you maintain security on the external files to ensure they are not altered unintentionally.

### To Be Continued

Our mission is still the same and will continue. Keep an eye out for future post that will show further examples of how you can use the dbatools module to make your life easier.

_Header image provided via [flickr](https://flic.kr/p/ckpHpL)_ | _Magic giphy via [giphy.com](https://giphy.com/gifs/reactiongifs-ujUdrdpX7Ok5W)_
