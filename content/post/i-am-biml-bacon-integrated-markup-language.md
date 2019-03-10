---
title: I am Biml (Bacon Integrated Markup Language)
date: 2014-11-03T06:00:00-06:00
drafts: false
---

Wouldn’t it be awesome if that is what it was really called? Maybe not, so what does Biml really stand for?

![](/images/bimllogo.png)

## Small Background

<a href="http://www.varigence.com/Company" target="_blank">Varigence</a> is the company that created Biml, particularly Scott Currie, back in 2008. You can check their page to get the full store, it is worth a read. It is a pretty remarkable story that they took a thought and turned it into a full technology that includes a proprietary and an open source product. I can remember hearing about it within the past year or so but it never clicked with me at the time (it does now). I think around 2012 it started to get an uptick in exposure. It has begun showing up in sessions at PASS Summit and at SQL Saturdays in some places more and more in the past year.

Now BimlScript is the use of C# (by default) code within your Biml that offers an enormous amount of flexibility into what you can do. This is where you can get into dynamically creating things within an SSIS projects or even SSAS projects.

## The Potential

I think back to a contract job I had with the Army handling ETL design. Through <a href="http://www.foia.gov/how-to.html" target="_blank">FOA request</a> I was responsible for making packages that would pull data out of the source and dump it into an Access Database or Excel spreadsheet. The design pattern I had to used there was creating a package per table of data that needed to be pulled and then a master package that would simply iterate through all of those “table” packages.

We used AGILE development process so one request would generally take me a few days to build out the project, deploy it into test, then staging, and then finally production. So depending on what amount of data was being requested it could take up to a week to get everything designed and finalized to send the file to the requestor.

If I could have used Biml for this process I would have cut down the initial design time considerably. With it providing me the ability using C# (which I would have had to learn as well back then) to iterate over the table list of a given source to generate all the Data Flow tasks; man think of the clicks you do just setting up one data flow task and how much time this would have saved.

## Biml Products

The most common product referenced in the community, at least that I have seen, with Biml is <a href="http://bidshelper.codeplex.com" target="_blank">BidsHelper</a>. Which BimlScript is one part of what is included in BidsHelper, there are a ton of little things that were added in there that creators of BIDS left off. If you are using SSDT-BI now a few of those things included may be obsolete possibly now. You can look at the <a href="http://bidshelper.codeplex.com/documentation" target="_blank">list under documentation</a> of what is included.

BidsHelper is something that is used with Visual Studio (BIDS or SSDT-BI) and is an excellent starting point to get started using Biml. If you find you need to go to the next step Varigence has an IDE they created called <a href="http://www.varigence.com/Products/Mist/Capabilities" target="_blank">Mist</a> that provides a very robust environment to develop SSIS and SSAS. I link to a few videos below that show off what this product can do, very cool stuff! The other product they have is <a href="http://www.varigence.com/Products/Vivid/Features" target="_blank">Vivid</a>, this is an add-on for Excel users that handle data analysis.

## Resources to Note

When I wanted to learn more about Biml I found myself asking, “where do I start?”. Similar to how a lot of folks ask when they want to go into being a DBA or Database Developer. Below are just some links to articles and videos that can help you get started.

## Articles:

- <a href="http://www.sqlservercentral.com/stairway/100550/" target="_blank">SQLServerCentral’s Stairway to Biml</a> (yes, you should register…just do it)
- <a href="http://billfellows.blogspot.com/search/label/Biml" target="_blank">Bill Fellow’s Blog post on Biml</a> (some good nuggets if you learn by seeing)
- <a href="http://bimlscript.com/GetStarted/InitialWalkthroughs" target="_blank">BimlScript Walkthroughs, Getting Started</a>
- <a href="http://varigence.com/Documentation/Language/Element/AstRootNode" target="_blank">Biml Language Reference</a> (similar to MSDN for SQL Server)
- <a href="http://varigence.com/Documentation" target="_blank">Biml Snippets</a> (ton of examples to learn from here)

## Videos that I found the most helpful:

- <a href="http://youtu.be/YeUbFfNQ-9o" target="_blank">SQLug.se - Peter Hansen's - Biml, session 1</a>
- <a href="http://youtu.be/pzNIyjTrnSg" target="_blank">SQLug.se - Scott Currie's - Biml, session 2</a>
- <a href="http://youtu.be/YeZesq29d9U" target="_blank">Using BIML as an SSIS Design Patterns Engine (PASS DW/BI Virtual Chapter)</a> (Andy Leonard does a great walkthrough of Biml)
- <a href="http://youtu.be/6DiuJxb49Gs" target="_blank">Biml Introduction and Fundamentals Webinar</a> (Peter Avenant with Varigence, great video showing Mist and Biml, you should subscribe to their channel)
- <a href="http://youtu.be/NJdsV8hu74Y" target="_blank">Working with BimlScript to ease and automate your SSIS development</a> (Session done by Jeff Mlakar, just this month. Some excellent tips and examples)
