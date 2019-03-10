---
title: "SQL Server Data Tools: A spork of sorts (part one)"
date: 2014-10-15T08:00:00-06:00
drafts: false
tags: [sqlserver]
---

Prior to SQL Server 2012 the Business Intelligence (BI) toolset was made up of just Business Intelligence Development Studio (BIDS). Easy to install as it was part of the SQL Server installation media. Now with database development tools you had to go the route of getting a license for Visual Studio where it allowed you to create database projects. Oh, how that is all changing now, and in some ways go back in time.

SQL Server Data Tools (SSDT) brought about changes in BI and database development. First **Database Development** changed to SQL Server Projects and no longer required a fully licensed version of Visual Studio, it used the integrated shell. It stayed this way up until Visual Studio 2013. With VS 2013 it now appears it might have gone back to requiring a licensed version of VS. A bit more on this part below.

**Business Intelligence development** also changed tools from BIDS to SQL Server Data Tools. Wait, wasn’t SSDT for database development? It is actually for both but actually require separate installs. It is now being referred to as SSDT-BI. Nice work there Microsoft.

If you have installed SSDT for SQL Server 2012 you will note that it actually is only installing SSDT-BI by viewing the new project window:

![](/images/spork1.png)

What?!!?? You want me to install the same thing again? Well it appears that even though they share the same title of application they are now separate. If you read the blog post on MSDN, <a href="http://blogs.msdn.com/b/ssdt/archive/2014/01/31/ssdt-and-visual-studio-versions.aspx" target="_blank">SSDT and Visual Studio Versions</a>, and note the comments. I particular liked this one:

![](/images/spork2.png)

What that means is SSDT is now something that encompasses two things: Database Development and BI Development (reference a fork + spoon = spork) but two different teams are developing each one. Glad that confusion is over.

Now if you go to the page for <a title="http://msdn.microsoft.com/en-us/data/hh297027" href="http://msdn.microsoft.com/en-us/data/hh297027" target="_blank">Microsoft SQL Server Data Tools</a> it will provide al ink to “Download Visual Studio 2013 with SQL Server Tooling” that basically points you to the Visual Studio 2013 product page. Which I have installed VS 2013 for Desktop and no where can I find how to make it update to include SQL Server Tooling. If you visit the <a href="http://www.visualstudio.com/en-us/products/compare-visual-studio-products-vs.aspx" target="_blank">Visual Studio 2013 production comparison to Visual Studio Online</a> and view under “Development Platform Support” you will notice that SSDT only shows up for Pro, Premium, and Ultimate Editions. So they went back to 2010? So right now it appears if you want to do database development stick with VS 2012 and down. I think VS 2012 includes support for SQL Azure development but I have not dove into that as of right now.

In the next post I will go over some things with SSDT-BI and how installation for this changed.
