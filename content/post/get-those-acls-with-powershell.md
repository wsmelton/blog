---
title: Get those ACLs with PowerShell
date: 2011-04-21T13:31:00-06:00
---

If I want to view the access permissions to a particular directory in Windows I can always go to the folder itself and check the security properties on the folder:

![](/img/securitytab.jpg)

But that is boring, lets use PowerShell!!!

The cmdlet (_commandlet_) of choice for this is going to be: <a href="http://technet.microsoft.com/en-us/library/dd347635.aspx" target="_blank">`Get-Acl`</a>

I will let you dive into this command and try to figure it out, but this is the one-liner I use most often that gives me the information I want to know about the SQL Server directory:

```powershell
$a = (Get-Acl -Path 'D:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL')
$a.Access | Select-Object FileSystemRights, AccessControlType, IdentityReference, IsInherited | ft -auto
```

Here is a screenshot of the output:

![](/img/folder_acl.jpg)

Now that is for a folder, what if I wanted to do it for a Registry hive as well? It works the same way with the exception of two things: (1) Your "Path" is changed to the registry hive of choice (HKLM, HKCU, etc) and (2) the "Select-Object" portion. Instead of "FileSystemRights" you would change that to "RegistryRights", like so:

```powershell
$a = (Get-Acl -Path 'HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server')
$a.Access | Select-Object RegistryRights, AccessControlType, IdentityReference, IsInherited | ft -auto
```

Here is screenshot of the output:

![](/img/hklm_acl1.jpg)
