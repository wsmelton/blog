---
title: What a few lines of code can do
date: 2011-08-01T08:00:00-06:00
draft: false
---

You find out PowerShell is fun when you start playing with it and actually try to perform a task with it. I have been using it the past few months to try and decrease the time it takes me to perform a scan of a SQL Server. What I mean by scan is I work with the IASE Security Technical Implementation Guide checklist (STIG). You can find the checklist for SQL Server <a href="http://iase.disa.mil/stigs/app_security/database/sql.html" target="_blank">here</a>, they have not published one for SQL 2008 so I just use the SQL 2005 checklist for now.

Anyway some of the findings in that checklist have you check configuration settings that could be checked through SSMS or through registry keys. I prefer to check registry keys or use SQL SMO if I can, cause guess what...PowerShell can do it for me.

I am not going to provide the complete script right now cause it is still a work in progress. I have a parameter required to pass with the script, the instance name. I was just using that to connect with SQL SMO, but now I have just figured out how I can use that with looking at the registry.

With a SQL Server installs (SQL 2005 and higher) it adds a registry hive of `HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server`. To really get deeper than that you have to know what the path is for the instance and it varies between SQL Server versions and default/named instances. In SQL Server 2005 it is `MSSQL.#` ("#" being a number between 1 - 9). With SQL Server 2008 it changed to `MSSQL10.<InstanceName>` and SQL 2008 R2 it is `MSSQL10_50.<Instance Name>`. So if you were working with a default instance the path for SQL Server 2008 and R2 would be `MSSQL10.MSSQLSERVER` or `MSSQL10_50.MSSQLSERVER`. With SQL Server 2005 it would be your best guess cause if there are multiple instances it will depend on the order it was installed. If the default instance was first it would be `MSSQL.1`, then any named instance after that would have that number incremented.

Needless to say it took me a few minutes to get it down right but this is the code I came up with, and there is probably another way of doing it (or even doing it with less). I have not tested it on every version of SQL Server. If I come across any bugs I will update this post.

_Note: `$InstanceName` is the variable used to pull in the parameter passed when calling the script._

```powershell
#find registry path to work with for the instance
$regInstance = (Get-ItemProperty 'HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server'.InstalledInstances

#build registry path to output according to instance name passed with script
if ($InstanceName -eq $env:COMPUTERNAME)
{
    #default instance
    $currentValue = $regInstance | Where-Object {$_ -eq "MSSQLSERVER"}
    $regPath = (Get-ItemProperty 'HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\Instance Names\SQL').$currentValue
    $fullpath = "HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\$regpath"
}
else
{
#named instance passed
    $currentValue = $regInstance | Where-Object {$_ -eq $InstanceName}
    $regPath = (Get-ItemProperty 'HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\Instance Names\SQL').$currentValue
    $fullpath = "HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\$regpath"
}
```
