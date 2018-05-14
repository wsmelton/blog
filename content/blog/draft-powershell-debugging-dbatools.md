---
title: Debugging dbatools
aliases: /debugging-powershell
date: 2017-08-07T02:00:00-06:00
drafts: true
tags: [dbatools]
---

## Keeping it Real

I thought it would be helpful to walk you through a true-to-life scenario that I had where I needed to debug the [dbatools module](https://dbatools.io). An [issue](https://github.com/sqlcollaborative/dbatools/issues/2012) was filed on the repository that pointed out in certain cases multiple login failed messages are written to the SQL Server instance passed into a command when a credential is provided. The login failure is generally showing as the Windows account running the PowerShell session (_powershel.exe_). The issue noted that in this case the environment did not allow the Windows account access to the SQL Server instance, hence the need to pass in a SQL Credential (or SQL Login).

The conundrum came in that this was not with every command. In this issue the user was using `Test-DbaIdentityUsage` and if he used `Get-DbaDatabase` he didn't see the same issue.

_Small note: I've had this post in draft for a few months now and the change implemented from this debugging scenario has sense been adjusted to another method._

## Setup

When you are debugging, and you are debugging a specific scenario, you need to setup the environment as close as you can to duplicate the issue. So in my case I needed to setup a few logins, one as a domain and another as a SQL Login each with specific permissions.

In this debug session I "borrowed" a lab environment from Chrissy ([@cl](https://twitter.com/cl)) as it was already setup with the specific SQL Server version I needed. The machine in use for this scenario was **sql2008**, and the domain is **BASE.local**. I'm use a separate machine to ensure it was a remote connection.

1. Created AD account [BASE\shawntest] that does not have access to the sql2008 instance.

![](/img/debug_dbatools_1.png)

2. Started VS Code as that AD account on the remote machine (will run command under this context)
3. Verified in the terminal that BASE\shawntest was returned with _whoami_

![](/img/debug_dbatools_2.png)

4. Created test login on sql2008 with sysadmin rights to be my "dba" account, this will be the credential I pass into the dbatools command.

```sql
USE [master]
GO
CREATE LOGIN [TestDba] WITH PASSWORD=N'MySecretPassword',
	DEFAULT_DATABASE=[master], CHECK_EXPIRATION=OFF, CHECK_POLICY=OFF
GO
EXEC master..sp_addsrvrolemember @loginame = N'TestDba', @rolename = N'sysadmin'
GO
```

5. Now before I started debugging I decided to just do a quick comparison on the two commands: `Test-DbaIdentityUsage` and `Get-DbaDatabase`. I knew right off that the issue was around how we build the connection for the command, so I focused on comparing that area of each command. I found one main difference between these two commands for that area:

 - The `-MinimumVersion` parameter is being used in `Test-DbaIdentityUsage` and not in `Get-DbaDatabase`.

6. I updated `Get-DbaDatabase` to utilize that same parameter and could replicate the same issue that Test command was having.
7. So I identified that the `Connect-SqlInstance` was the exact command I need to debug.

### Connect-SqlInstance

A bit about this specific command before we move on. This is an internal command that is utilized in dbatools to build an SMO connection to a given instance. It does a lot of things and is one of those commands we do not change often, since it is used by any command that has to connect to SQL Server.

The `MinimumVersion` parameter was added to more easily control how we handle commands that only need to work with specific versions of SQL Server. For example, the Availability Group commands won't work on anything less than SQL Server 2012. So in those commands we set that `MinimumVersion` to 11, meaning that if you pass in a SQL Server 2008 R2 instance to the command it spits out a message that the version is not supported.

## Dot Sourcing Module Code

When you debug a module the debugger has to be able to reference the code in that module. This requires that the code is dot sourced into your debugging session. A special thing the module does by default (to save time on importing) is it loads the files into memory using `System.Io.File`, which is much faster than dot sourcing.

In that effect it was impossible to debug the dbatools modules since they files were not being dot sourced. So our local magician adding functionality for me that would allow us to debug the module more easily.

### Debugging Parameter for dbatools

At this time to debug the module you need to set a variable to true in your PowerShell session: `$dbatools_dotsourcemodule = $true`. Setting this global variable will cause the code in the module to be dot sourced so we can run the debugger.

![](/img/debug_dbatools_3.png)

## Into the Weeds

So set this up I simply took the `Get-DbaDatabase` command and set a breakpoint on the `Connect-SqlInstance` statement of that command. I started the debugger in VS Code as an interactive session, just my preferred method. [I went over using debugging with VS Code in [my previous post](2017-10-30-powershell-debugging.md) if you need a refresher.]

So my command I ran in the interactive session was:

```powershell
Get-DbaDatabase -SqlInstance sql2008 -SqlCredential $myCred
```

The `$myCred` contained that SQL Login I created earlier, _TestDba_.

When the breakpoint was hit I simply **step-into** the `Connect-SqlInstance` command and then step through it to see what is going on.

Cool part of debugging with VS Code is you can hover over a variable and see the contents of it:

![](/img/debug_dbatools_4.png)

![](/img/debug_dbatools_5.png)

So the key item I found was when we build the server object in SMO we are passing in the name of the instance received. This is when the login failed messages are being hit on a given instance. You can see from the screenshot below that I have stepped to the statement on line 154, so the statement on line 153 has already been executed. This line is **before** we actually pass in the credential.

![](/img/debug_dbatools_6.png)

So you can see on the left side the true login value is null, meaning we have not passed that in yet, and the command went ahead and tried to login with the context of the user running the PowerShell session. The additional issue is that any line that called on that `$server` variable was causing additional failed logins to hit the sql2008 instance.

![](/img/debug_dbatools_7.png)

The issue with the MinimumVersion parameter was it was being checked before we actually made a connection in SMO. So that was an easy fix by just moving that section of code immediately after we make a connection.

So we have two issues with the following line:

```powershell
$server = New-Object Microsoft.SqlServer.Management.Smo.Server $convertedSqlInstance.FullSmoName
```

- Passing in the server name is going to cause SMO to make an initial connection to the instance.
- Not passing in a value at all will cause it to make an initial connection to `localhost`.

So as just a hot fix at the time was to pass in a false value. This ended up after testing causing a few issues elsewhere with output.

![](/img/debug_dbatools_8.png)

Header image provided via [pixabay](https://pixabay.com/en/fly-swatter-flyswatter-fly-flap-bug-149265/)