---
title: How do I open PowerShell? And something else too…Part 2
date: 2010-08-01T23:00:00-06:00
draft: false
---

This is a two part post on me opening PowerShell and then finding out something peculiar…You can see part one <a href="/2010-07-30-how-do-i-open-powershell-and-something-else-toopart-1" target="_blank">here</a>.

In the previous post I left you with the Jump List that shows for the Windows PowerShell window when you right-click the program in the taskbar:

The “Import system modules” caught my fancy. Now most of the things I have read on PowerShell from blogs and such speak of <a href="http://msdn.microsoft.com/en-us/library/ms714450(VS.85).aspx" target="_blank">snap-ins</a> and not necessarily <a href="http://msdn.microsoft.com/en-us/library/dd878310(VS.85).aspx" target="_blank">modules</a>.  Although they are both things that you can create and customize in PowerShell.

So I went to TechNet to get a definition of both, <a href="http://technet.microsoft.com/en-us/library/dd745031(VS.85).aspx" target="_blank">here</a> first. So my synopsis of the definitions is that a snap-in is something that implements <a href="http://technet.microsoft.com/en-us/scriptcenter/dd772285.aspx" target="_blank">cmdlets</a> and <a href="http://technet.microsoft.com/en-us/library/dd347723.aspx" target="_blank">providers</a>.  Then a module is (among other things) something that can organize and distribute cmdlets and providers.

So (here comes some of the peculiars), click on this option in the Jump List and you will notice the UAC prompt (user access control) that pops up in Windows 7 warning you that Administrative privilege is fixing to be used. Then a new PowerShell prompt opens up and you see something similar to this:

![](/img/importsystemmodules_thumb.jpg)

So it goes through and loads the modules.  Which you may ask how does it know what modules to load? Well if you go look at the directory `C:\Windows\System32\WindowsPowerShell\v1.0\Modules` you will find out.

Uh…SQUIRREL!!! Side note here, you notice it shows v1.0 as the directory when everything you read tells you v2.0 was integrated into Windows 7 and Window Server 2008 operating systems…well that v1.0 is there for backward compatibility.  You are running 2.0 of the console. [Thanks to Nicholas Cain (<a href="http://www.englishtosql.com/" target="_blank">blog</a> `|` <a href="http://twitter.com/anonythemouse" target="_blank">twitter</a>) for <a href="http://serverfault.com/questions/73410/how-to-uninstall-windows-powershell-v1-0-on-windows-7-rtm" target="_blank">pointing</a> me in the right direction on this one.]

First, once that gets done type in the command: `Get-Module –ListAvailable` and you will get this list:

![](/img/importsystemmodules_moduleslist_thumb.jpg)

Now all this is under the context of running the prompt under the Administrator, so if I open another shell window those modules are not loaded…or are they? So I open up another prompt, that opens with my username, and execute the same command and I receive this list:

![](/img/importsystemmodules_moduleslist_myacct_thumb.jpg)

Not much difference here, other than the additional ExportedCommands that show up for PSDiagnostics. Peculiar…so since modules can be used to control snap-ins I next wanted to see what snap-ins changed between each session as well.

Administrator session snap-in list

![](/img/importsystemmodules_snapinlist_admin_thumb.jpg)

My username session snap-in list

![](/img/importsystemmodules_snapinlist_me_thumb.jpg)

Notice the two new ones that show now, again this is after clicking on the “Import System Modules” from the jump list for Windows PowerShell program pinned to my taskbar?  Well if you did not catch it, the Administrator session now has access to the SQL Server 2008 snap-ins.  They only show up after clicking the import command.  Which these snap-ins are available because I have SQL Server 2008 Management Studio installed on my desktop.

Now…I just read over what I typed out above and on the previous post. It does not look that important probably to a normal person (cause I don’t claim to be normal, ask my wife). However, it was interesting enough to me that caused me to learn more about what modules and snap-ins are for, and mostly what happens when you click on “Import System Modules”.

The only question I still have is why would Microsoft give me a shortcut in this manner that I can’t use!!??!! If clicking on this option in the jump list changes the context of my session to Administrator AND opens it in a new window, then I just lost my ability to connect to remote computers through the shell under my username.  If doing this on my desktop it will open as the local Administrator, so I can’t connect to my lab domain running under VMWare Server. Plus I loose my command history from my original window.

Don’t feel lost, there are ways to customize your profile for PowerShell to have it load all these modules, snap-ins, and other things at the time you open the window.  I would tell you how to do that, but I’m still learning that portion of it myself.
