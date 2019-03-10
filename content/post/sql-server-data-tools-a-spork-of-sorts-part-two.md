---
title: "SQL Server Data Tools: A spork of sorts (part two)"
date: 2014-10-20T08:00:00-06:00
drafts: false
tags: [sqlserver]
---

In the previous post (a bit of a rant too) I went over SSDT and how it has evolved for whatever reason by Microsoft into SSDT (Database development) and SSDT-BI (Business Intelligence development). In this post I wanted to go over how you actually get this installed so you can start the fun work of working with SQL Server 2014.

If during the CTP phases of SQL Server 2014 releases you may have caught the blog post on <a href="http://blogs.msdn.com/b/mattm/archive/2013/07/02/sql-server-data-tools-business-intelligence-ssdt-bi-for-sql-server-2014-ctp1.aspx" target="_blank">SQL Server Data Tools – Business Intelligence (SSDT BI) for SQL Server 2014 CTP1</a> (another interesting post to read response to this in the comments). This is where it was told that you will not be able to install SSDT BI on a new machine with SQL Server 2014 installation media. It became a separate download. You would get this download from <a href="http://msdn.microsoft.com/en-us/data/hh297027" target="_blank">Microsoft SQL Server Data Tools</a> page on MSDN, scroll down to the bottom of the page to find SSDT-BI download links for VS 2012 and VS 2013.

 I opted to just go ahead and move to Visual Studio 2013 version and downloaded that from <a href="http://www.microsoft.com/en-us/download/details.aspx?id=42313" target="_blank">here</a>. If you have installed the version for VS 2012 before it has not changed from that installation process. I will go over the installation for VS 2013 version to just provide a walkthrough for those that may be just starting out.

 You start out with a file named “SSDTBI_x86_ENU.exe", yeah no 64-bit version still. After the download is complete just double click. Now this is a basic clicking next through the wizard and I will just point out a few notes from my experience installing this on a new Windows 7 machine.

- The file downloaded is going to extract the files to a directory of your choice. If you end up having to cancel and start over, you go into that extracted directory and run the setup.exe file. You are actually going to get the SQL Server Installation Center similar to this:

![](/images/spork_p2_1.png)

Just click on “New SQL Server stand-alone installation…” and it will bring you to the starting point of accepting the license terms.

- It states in the feature selection that .NET Framework 4.5 is installed through this media. In my instance it actually did not install this and failed with a feature rule check. Might be worth verifying that is installed if you are on a new machine.

![](/images/spork_p2_2.png)

- Also note above what it is also going to install, Visual Studio 2012. If you don’t believe it, check out my own laptop:

![](/images/spork_p2_3.png)

Once you get done with the installation you are ready to get started with Business Intelligence development.

![](/images/spork_p2_4.png)

Happy learning!
