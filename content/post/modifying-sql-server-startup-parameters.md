---
title: Modifying SQL Server Startup Parameters
date: 2015-12-02T08:00:00-06:00
drafts: false
tags: [sqlserver,powershell,scripts]
---

<a href="https://youtu.be/8s3C1him6Lk" target="_blank">Mike, Mike, Mike, Mike, Mike</a>....guess what I figured out? Well it all started by reading Mike Fal's post on <a href="http://www.mikefal.net/2015/12/01/managing-sql-server-services-with-powershell/" target="_blank">Managing SQL Server Services with #PowerShell</a>. In that post he goes over manipulating the SQL Server service account and how to update it. In my case I needed to create a script that would let me alter the Startup Parameters.

If you go search right now for using PowerShell to alter the startup parameters for SQL Server...go ahead....you mostly saw post for modifying the registry keys that hold the values. I was not fond of doing this because I knew it could be done using the same method (well not exactly) that Mike's post discusses. The class used in SMO for the services have methods that easily let you manipulate the Service accounts, but the startup parameters are simply a property of the object <a href="https://msdn.microsoft.com/en-us/library/microsoft.sqlserver.management.smo.wmi.service.aspx" target="_blank">Microsoft.SqlServer.Management.Smo.Wmi.Service</a>.

If you did not know this when you look at MSDN for the properties of a class you can find out which properties can be manipulated. They will start out with one of two phrases:

- "Gets the..." = You can only read this property
- "Gets or sets the..." = You can read and change the property.

Low and behold the StartupParameters property is one that can be read and set. So how do you set it? Well the one thing to remember is you DO NOT need to remove what is already in that property because IT WILL BREAK YOUR SERVER!

Let me be clear, setting the property means you need to append to what is already there, so don't just go setting it equal to something like "-T1118". Doing this will remove the required parameters to start SQL Server itself, and no it will never warn you of this...so proceed at your own risk.

So all I wanted to do was append some additional startup parameters that I add to any server build I do, or touch after the fact:

- 1118
- 1117
- 3226

To do that I simply run this bit of code:

```powershell
$server = 'MyServer'
$sqlservice = "MSSQLSERVER"
$sqlagentservice = "SQLSERVERAGENT"
$flagsToAdd = ";-T1117;-T1118;-T3226"

Add-Type -AssemblyName "Microsoft.SqlServer.SqlWmiManagement,Version=11.0.0.0,Culture=neutral,PublicKeyToken=89845dcd8080cc91"
$sqlwmi = New-Object Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer $server
$wmisvc = $sqlwmi.Services | where {$_.name -eq $sqlservice}
$wmisvc.StartupParameters = $wmisvc.StartupParameters + $flagsToAdd
$wmisvc.Alter()

$wmisvc.Stop()
Start-Sleep -seconds 15
$wmisvc.Start()

$wmiAgent = $sqlwmi.Services | where {$_.name -eq $sqlagentservice}
$wmiAgent.Start()
```

Now the last bit for starting SQL Agent is because when I stop SQL Server it will also stop any dependent service.

One thought I also had was "what if I want to remove a trace flag?", that was say just added by accident, or in troubleshooting? You simply do a replace for the property and just modify the line for setting it to be:

```powershell
$wmisvc.StartupParameters = $wmisvc.StartupParameters.Replace(";-T1118",'')
```

Now some folks might see the risk in using this method, but to me it is just as risky changing some registry key. If you get the wrong format SQL Server will not start back up, but it is generally going to give you a clear message in Event Viewer that the parameters are the issue. Just be careful, and test it before using it.
