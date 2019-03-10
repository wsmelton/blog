---
title: SSDT–Importing Script Does Nothing
date: 2013-02-18T07:00:00-06:00
draft: false
---

I have been working with <a href="http://msdn.microsoft.com/en-us/data/tools.aspx" target="_blank">SSDT</a> the past few months at my day job, in order to get a database versioned. I am also trying to use it for a few things with a side job as well.

So, a simple task to start with is create a new SQL Database Project, and import a script (.sql) file to bring in all the database objects. You would think it was simple until you go through the process, get no errors and no objects in your project.

![](/images/importmenu_thumb.jpg)

![](/images/importscriptfinish_thumb.jpg)

Mother Hubbard, what the heck is the matter? No errors, and the summary log does not give any help either. Well, I got curious so I opened up the script in Visual Studio and received this message:

![](/images/importproblem_thumb.jpg)

Select “Yes”, and then save the file. Repeat the steps above and voila it works, at least for me. You will also notice it took a good bit more time to complete.

![](/images/importsuccess_thumb.jpg)
