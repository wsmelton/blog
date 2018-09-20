---
title: Windows 10 and SSCM disappearing
date: 2015-12-11T08:00:00-06:00
draft: false
---

I have been using Windows 10 since it was released on my main (well only) laptop. I found some issues with the SQL Server management tools through the upgrade process, specifically SQL Server Configuration Manager (SSCM). The issue I had was SSCM disappearing from the Start Menu when I upgraded to Windows 10. I also had a repeat of this issue after applying the <a href="https://support.microsoft.com/en-us/kb/3116908" target="_blank">latest update to Windows 10 for December 2015</a>.

Why it does this I have not found as of yet but it is easily fixed. The "Microsoft Common Console Document" or msc files for SSCM are stored under `C:\Windows\SysWOW64`.

![](/img/mscfilesforsscm.jpg)

If you want to just create new shortcuts, right-click each one and send to your desktop. You can then just move those shortcuts, after renaming them if you wish, to `C:\ProgramData\Microsoft\Windows\Start Menu\Programs` and go into the appropriate folder for your version of SQL Server.

I did find that for some reason the 2016 preview of SSCM (SQLServerManager13.msc) no longer functions. I get a WMI provider error when I try to use that version of SSCM.
