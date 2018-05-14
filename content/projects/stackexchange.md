---
title: StackDb PowerShell Module
tags: [scripts]
---

Maybe you are tired of AdventureWorks or if you are still old school with Northwnd and Pubs? Brent Ozar has for many years now been using [StackOverflow database]("http://www.brentozar.com/archive/2014/01/how-to-query-the-stackexchange-databases/") in his training and demos. As StackExchange (SE) started providing public [archives of the SE network sites]("https://archive.org/details/stackexchange").

I wanted to be able to build out a sample database on all of these archives as I needed, so wrote a PowerShell module.

# Where to get it?

You can find the files in my GitHub repository, [PSStackExchangeDb](https://github.com/wsmelton/PSStackExchangeDb).

# A short example...

```powershell
<# Refresh module in cache to get latest #>
#rmo PSStackExchangeDb
ipmo C:\GitHub\PSStackExchangeDb\PSStackExchangeDb.psd1

<# See if site exist and what file size is #>
Get-SEArchive -siteName woodworking -listAvailable

<# download archive file #>
Get-SEArchive -siteName Woodworking -downloadPath C:\temp\SESites -Verbose

<# export 7z file #>
Export-SEArchive -filename C:\temp\SESites\Woodworking.stackexchange.com.7z -Verbose
# see files
Get-ChildItem C:\temp\SESites\Woodworking.stackexchange.com

<# Create database and import data from xml files #>
# Create database (must not already exist)
New-SEDatabase -sqlServer manatarms -databaseName Woodworking -Verbose
# Import xml files
Import-SEArchive -filepath C:\temp\SESites\Woodworking.stackexchange.com -sqlserver manatarms -database Woodworking -Verbose

# Or if want to reload specific table (purge it first)
Invoke-Sqlcmd -serverinstance manatarms -database Woodworking -Query "DELETE FROM Posts"
Import-SEArchive -filepath C:\Temp\SESites\Woodworking.stackexchange.com -sqlserver manatarms -database Woodworking -tableList 'Posts'
```

Recording of the above code:

<video src="/img/PSStackExchange_Example_Woodworking.mp4" width="600" height="400" controls preload></video>