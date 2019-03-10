---
title: SQL Server Prerequisites .NET Framework
date: 2014-10-02T07:00:00-06:00
drafts: false
tags: [sqlserver,powershell]
---

As of SQL Server 2012 the <a href="http://msdn.microsoft.com/en-us/library/ms143506.aspx" target="_blank">.NET Framework prerequisite</a> of .NET 3.5 SP1 is no longer installed for you by the SQL Server installer if it is found to be missing from the server. Now with Window Server 2008 R2 SP1 or higher this is simply enabling the feature within Windows Server, no actual installation. This can be easily accomplished with PowerShell as a quick script to run prior to doing the installation of SQL Server.

The PowerShell Windows cmdlet that is used in this instance will be:

   - <a href="http://technet.microsoft.com/en-us/library/jj205469.aspx" target="_blank">`Get-WindowsFeature`</a>
   - <a href="http://technet.microsoft.com/en-us/library/jj205467.aspx" target="_blank">`Install-WindowsFeature`</a>
(Windows Server 2008 R2 you will use <a href="http://msdn.microsoft.com/en-us/library/ee662309.aspx" target="_blank">`Add-WindowsFeature`</a>).

The .NET 3.5 SP1 feature in Windows Server is referenced as `Net-Framework-Core` in PowerShell. You can find this by calling the command:

```powershell
Get-WindowsFeature Net*
```

![](/images/netframeworkcore_ps.png)

The below script is going first verify it is not installed and then will enable the feature (or technically install it I guess). In order to do this though you will need the OS media as you have to pass in the source path to `<drive letter>:\sources\sxs`. **Note: You have to execute this in an elevated PowerShell console, so "Run as Administrator".**

```powershell
#verify installed first
(Get-WindowsFeature Net-Framework-Core).Installed

#Add feature
Install-WindowsFeature Net-Framework-Core -source 'G:\sources\sxs'
```

When you run this command you will see a status "bar" of sorts appear while it is performing the installation. Once completed you should see output that lets you know it was successful.

Now if you happen to see any errors you might reference the <a href="http://support.microsoft.com/kb/2734782" target="_blank">KB 2734782 - .NET Framework 3.5 installation error</a> as there are various reasons why this command might fail.

### A small update to this post...

I recently came across a server that I was getting the `0x800f0906` error and went through the article above verifying Internet access from the server and having mounted the ISO for the OS properly. I came across a blog post that brings up the possibility that you need to <a href="http://blogs.technet.com/b/joscon/archive/2012/11/14/how-to-update-local-source-media-to-add-roles-and-features.aspx" target="_blank">update the local source media</a> on the server.
