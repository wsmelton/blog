---
title: "Check-InstanceConfig (part 1)"
date: 2013-12-04T09:00:00-06:00
drafts: false
tags: [powershell,sqlserver]
---

I was reading a blog post Mike Walsh published on Linchpin People last week: <a href="http://www.linchpinpeople.com/check-sql-server-configuration/" target="_blank">SQL Server Configuration Check Script</a>.

In that script he is, as the title says, checking the configuration of a SQL Server instance for particular things like those options not set to default values and a few particular ones that still are set to default. I was intrigued by this and by the time I got to the end of the blog post was like “bet I can do that in PowerShell too”. I had a slow weekend with the holidays so thought I would sit down and see what I could come up with.

Well I came up with two specific things that I wanted to accomplish with this script:

- Provide a reference point to the configuration options for each version of SQL Server
- Provide a function that will take that reference point and validate it against any instance

If I tried to put all the information I want to help explain the script this blog post would be longer than you have the time to read through. I decided to just break it up into two parts based on the list above. So this post will just be on the reference point I wrote and hopefully by the end you will have learned the following things:

- How it was written
- What it contains
- A few examples

### A few caveats about the script

I did not do anything special in PowerShell that is specific to any particular version. This script should work on PowerShell 2.0 and higher. You will notice if you open this script up in the PowerShell ISE 3.0 or higher I did use <a href="http://www.powershellmagazine.com/2013/01/14/pstip-use-custom-regions-to-fold-code-in-powershell-ise-3-0/" target="_blank">regions</a>, just a formatting feature in the ISE. It is treated as normal comment lines outside of the ISE.

There is more than one way to do things in PowerShell, this is just the way I decided to go. As well I did not cut corners in this script. I wanted to make sure every command and variable was understood. I tried to not use any aliases with commands (e.g. “?” instead of `where` or `where-object`).

### How it was written

The first section I put in the script was a comment block that contains the BOL links for the “Server Configuration Options (SQL Server)” page of each version:

![](/img/check_instance_1.png)

I went back and forth a few times on how to actually build out a list of the configuration option names and default values based on the current versions of SQL Server that are available. I knew I needed the information in order to validate it against a SQL Server instance, no matter what version I might try. In Mike’s script he simply scripted out temporary tables with this information. So I kept to the same concept and decided to use a **data table** (<a href="http://msdn.microsoft.com/en-us/library/system.data.datatable(v=vs.110).aspx" target="_blank">System.Data.DataTable</a>).

### What it contains

I tried to make the columns self-explanatory so the column naming convention I chose:

- `ConfigOption` – name of the configuration option in <a href="http://technet.microsoft.com/en-us/library/ms188787.aspx" target="_blank">`sp_configure`</a> or <a href="http://technet.microsoft.com/en-us/library/ms188345.aspx" target="_blank">`sys.configurations`</a> with new versions of SQL Server. The list contains those configuration options available from SQL Server 2014 to SQL Server 2000, as stated in the associated links in BOL for each.
- `Default_<4 digit year of SQL Version>` – there is a column for each version of SQL Server the script will support (e.g. `Default_2012`). If a ConfigOption name is not supported or included in any particular version this value is set to –9 (negative nine).

![](/img/check_instance_2.png)

An example of the –9 usage, “access check cache bucket count” is a configuration option only available in SQL Server 2008 and higher:

![](/img/check_instance_3.png)

### A few Examples

Ok, I am going to assume the reader is already familiar with <a href="http://technet.microsoft.com/en-us/library/ee176949.aspx" target="_blank">how to run PowerShell scripts</a>. I prefer the dot sourcing method in most cases. You can also simply copy and paste this into your profile if you desire. Remember, <a href="http://technet.microsoft.com/en-us/library/hh849920.aspx" target="_blank">Out-GridView</a> is your friend.

- To list out the complete data table execute this command: `$sqlConfigDefaults | Out-GridView`

![](/img/check_instance_4.png)

- I have variables already in the script to list out each version (reference lines 723-729 in the script). So if you wanted to list out the options for SQL Server 2014: `$sql2014_Defaults | Out-GridView`

![](/img/check_instance_5.png)

I could have filtered out the columns for the other versions, but I thought it to be a nice reference point to see those options that are still around from lesser versions. You can adjust this if you wish, but note that these variables are utilized in the function as well.

Here is the <a href="https://github.com/wsmelton/scripts/blob/master/posh/Check-InstanceConfig.ps1" target="_blank">full script</a>. This link will always point to the current version of the script. My next blog post will explain the function in the script.
