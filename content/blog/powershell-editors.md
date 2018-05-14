---
title: PowerShell Editors
date: 2016-10-19T22:00:00-06:00
draft: false
---

PowerShell Editors are the bread and butter in the life of an individual that wants to write PowerShell, whether for serious development or just starting. You could also be ready to get involved in open source projects around PowerShell, [they do exist](https://github.com/trending/powershell). [There is even one specific to SQL Server on GitHub.](https://github.com/sqlcollaborative)

What we use to write scripts in is another tool in our belt, with the main purpose of making development of said scripts more efficient, or even easier. You may have just been using Notepad or Notepad++ all your career, and want to take the next step. I have found certain areas to be important when I'm considering changing editors or things I look at most when testing a new one:

- syntax highlighting
- intellisense
- add-ons/extensions options
- footprint

## syntax highlighting

This matters more than you might think if the only thing you have used is Notepad. I open up a script that is hundreds of lines (or into the thousands) at times. When I try to debug it, having all the keywords or patterns of code color-coded makes it much easier on the eyes. It offers the ability to easily pick out the variables used in the script, or locating the comments (inline or blocks) (e.g. in SSMS comments are generally green). _Because everyone comments their code right._

## intellisense

If you are just learning a language (e.g PowerShell, T-SQL, .NET, etc.) intellisense can help with learning syntax and exploring the various classes or methods in a command. At times I have found this feature to get in my way, but it depends on how it is implemented in the editor. The main thing to be aware of on this feature is how it refreshes the cache. First thing I always do is learn the keyboard shortcuts for the intellisense.

SSMS is a good example, if you have 2 query windows open and in one window you created a table in a database. The second query window with SSMS will not know about that object, until you refresh the intellisense cache (CTRL + SHIFT + R). In the same area it is also important that the syntax check in the tool can pick up object references, that may not have been created yet, within the same file. If you have one large in-line script that you create objects at the start, and later on utilize those objects, it helps when the editor is smart enough to pick up the references correctly....compared to showing a bunch of red squiggle lines.

## add-ons or extensions

This is where you get into stuff that may be particular to the language or project you are coding. You may have preference for building snippets (e.g. try/catch blocks, if/else, etc.), or an extension that lets you build templates. In other areas it could be if it integrates with the tools used in your environment or development process (e.g. TFS, GitHub). It is not a show stopper in most cases if you have to use a separate tool to complete a particular task, but can be more efficient use of time if one editor has it over others.

## footprint

When I say footprint, I'm not necessarily referring to storage used but more memory and CPU usage. If the editor sucks up most of my memory and CPU (whether it creates excessive amount of threads or multiple processes), then it has the potential to interfere with me handling multiple task at once. Visual Studio (VS) is an example here, if you ever worked with VS 2008 or 2010 you understand how much those versions drained a machine of resources...and how long they took to open. Microsoft over time and each new version is getting much better at making the footprint for VS more efficient, if not smaller. I hear that VS next release (as of preview 15) is going to be a large improvement in this area.

## main players

PowerShell is growing in usage and that has helped the options for editors grow a bit as well, although there are still only a few main players in my opinion. I'll list out the main ones I see right now in the free market. In the market of you buy what you get the only one I have watched is [Sapien's PowerShell Studio](https://www.sapien.com/software/powershell_studio), it is a good tool for the money and offers many features.

### Windows PowerShell ISE

Just for notable mention, you have PowerShell ISE available (for free) in most current version of Windows. It is a good editor that meets all of my areas noted previously, just does not have that extra bit of magic I want. I do use this regularly in client environments when I need to troubleshoot or develop on a dev server (most environments I don't have access to desktop OS).

### Microsoft Visual Studio Community Edition

Starting with Visual Studio 2013, Microsoft changed their Edition options to include a Community Edition. This is basically offering the free version of what used to be considered the Pro Edition. This opened up the door to many things with add-ons and extensions. If you ever used VS Express Edition you recall that any 3rd party extension would never run. Now you can use any 3rd party extension that you want offered for VS.

In the area of PowerShell the main extension I use is [PowerShell Tools for Visual Studio](https://visualstudiogallery.msdn.microsoft.com/c9eb3ba8-0c59-4944-9a62-6eee37294597) (love this extension). It provides support to use the Solution/Project module in VS and syntax highlighting and intellisense for PowerShell.

The other extension I use is GitHub for Visual Studio, especially since I have started contributing the PowerShell repos on GitHub. It comes in handy to be able to stay in one tool to sync, commit, submit PRs, etc. compared to going into GitHub Desktop Client.

### Microsoft Visual Code

This product is free, and open source. The main thing that came with this product is it supports Apple's macOS and Linux flavored OS's. It does take getting used to the fact that you work with extensions more for various things, compared to it offering things as "built-in" features. It also has an extension for supporting syntax and some intellisense around PowerShell, not the best but it is getting better. It is a nice step above Notepad++ but not quite like VS, which I hope it never gets like VS.

It is much more lightweight than VS, for obvious reasons being that it does not support the whole solution and project templates. It works on folders compared to a project and solution file. So if you store all your scripts in a folder, opening up that folder will allow you to easily access all of your scripts from within tabs.

It does offer debugging and integration with Git. The Git integration works well, once you get used to how it does work. I do find though it is missing the ability to switch between remote branches for GitHub. So if you might be working on multiple things with branches for a repo I don't see it being usable right now. The debugger I have not used for PowerShell as of yet, tried but never could get it set right where it would work properly. If I do I will be sure to blog about it.

### Sublime

[Sublime](https://www.sublimetext.com/) is similar to Notepad++ on RedBull. Well, not really, it is an editor that offers many features for various languages. A good all around editor if you have to work with different coding languages. It is a paid tool, about $70 USD. This uses packages for add-on support, and does have [one for PowerShell](https://github.com/SublimeText/PowerShell) available. It is an open source repo however so may not be complete as what Microsoft tools offer.

## Bottom of the Pile

Starting out there used to be a few vendors that offered up some editors that I thought showed some promise, but as of today they have fallen flat for me. However, for completeness I will note them below just so you are aware of your options.

### Dell's PowerGui

[This tool](http://www.dell.com/us/business/p/dell-software-powergui/pd) flat out tanked after Dell purchased Quest Software. It had some much potential because it offered various packs for Active Directory, IIS and SQL Server. However, you will be hard pressed to even find documentation for it on Dell's site now a days. I really don't know why Dell even bothers to keep up online, it has so many bugs reported for it. I would suspect as Windows moves along there will be a version of the OS that PowerGui will not install.

### Idera's PowerShell Plus

[This is another tool](https://www.idera.com/productssolutions/freetools/powershellplus) that while still usable has seemed to be on the decline of use. There was a pretty big [community involvement](http://community.idera.com/powershell/) around this tool for some time, offering various modules and snippet libraries. You can see from that site now that it has been about a year since the last snippet or module has been posted.

# Sum of All Editors

To just sum everything up, in my opinion, Microsoft's options are at the top of the choices with regards to PowerShell Editors. It is though up to you to chose which ones you want to work with, choose the one you like and one that helps you get to scripting.

_[Header image source](https://flic.kr/p/7NFTF6)_

The content of this post can also be found [here](https://www.pythian.com/blog/Powershell-Editors).
