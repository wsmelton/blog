---
title: Improve Load Time on SQLPS
date: 2015-11-16T07:30:00-06:00
drafts: false
tags: [sqlserver,powershell]
---

Over the month of November a fellow PowerShell enthusiast, Mike Fal (<a href="http://www.mikefal.net" target="_blank">blog</a>`|`<a href="http://twitter.com/mike_fal" target="_blank">@Mike_Fal</a>), did a <a href="http://www.mikefal.net/tag/sqlps/" target="_blank">series on the SQL Server PowerShell module</a> (SQLPS). In reading his series curiosity struck on what the module does when it was loading. I also just <a href="http://www.mikefal.net/tag/sqlps/" target="_blank">answered a question on DBA.SE</a> that I figured out by tweaking a particular file for this module, so thought I would share more details.

_**WARNING: You are modifying the files at your own risk. You have been warned.**_

If you are not familiar with the files involved with a module, you can read more on that <a href="https://technet.microsoft.com/en-us/library/dd878324(v=vs.85).aspx" target="_blank">here</a>. The file I found most interesting is the "<em>SqlPsPostScript.PS1</em>" file, located in the SQLPS module folder for the given version of SQL Server:

```
C:\Program Files (x86)\Microsoft SQL Server\<version>\Tools\PowerShell\Modules\SQLPS\
```

This file is being called after the module is loaded as a nested module. You can find all of this by reading through the manifest file for SQLPS, `SQLPS.PSD1`.

The post script file does a handful things:

- Sets the location of your session to SQLSERVER:\ (the provider)
- Has a function that does the same thing, if you just enter "SQLSERVER:" at the prompt instead of typing the Set-Location. Could be a waste of 47 characters to me.
- Loads the DAC assemblies for managing and creating DAC packages with PowerShell.
- Loads the SQLAS module, if not already loaded.

Now the most annoying thing I always have with the SQLPS module is that it puts me in the location of the provider after it loads. I stop that by simply commenting out that first line in the file. A `Measure-Command` on loading the module before and after, shaves off a whole second (time is money).

The other thing I found was the warnings on the WMI service the poster on DBA.SE was getting, was strictly due to the SQLAS module being loaded. Which in the documentation I linked to in that question shows that this module utilizes WMI. Which that begs the question for Microsoft: Why you put WMI management into SQLAS, and not SQLPS?

Now the module itself when loading also loads numerous DLL files, which all those contain the magic that is SQLPS.
