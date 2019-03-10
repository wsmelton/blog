---
title: View server-level permissions in SSMS
date: 2012-01-10T08:00:00-06:00
draft: false
---

I was tooling around in SSMS the other day. In this particular instance I was granting a login instance-level permissions to test out a third party application at work. I did not want to give it sysadmin privileges for this so I just started out with giving it `VIEW SERVER STATE` (which most DMVs require in order to query them) and `VIEW ANY DATABASE`. [If you have never heard of these permissions, check out this little tidbit of info <a href="http://www.mssqltips.com/sqlservertip/1714/server-level-permissions-for-sql-server-2005-and-sql-server-2008/" target="_blank">here</a> from Brian Kelley (<a href="http://www.truthsolutions.com/" target="_blank">b</a>`|`<a href="http://twitter.com/kbriankelley" target="_blank">t</a>).)

Ok now that you have read that, you saw the T-SQL code to find the server-level permissions granted to any account on an instance of SQL Server 2005 or 2008. Well what if I only wanted it for one login and I wanted to use the GUI? Ah, ha!!!

So on my test system at home I have `[myUser]`, with the current permissions showing below (retrieved using Brian’s T-SQL code).

![](/images/current_perms_thumb.jpg)

Now I am going to grant the account `VIEW SERVER STATE` and `VIEW ANY DATABASE`. Running the T-SQL code again will show you this:

![](/images/new_perms_tsql_thumb.jpg)

Now you see this using SSMS by going to the properties of your login you are interested in, click on “Securables” in the left pane. You should see this window:

![](/images/securables_empty_thumb.jpg)

Now click on the “Search” button. You are presented with options as to what objects you want SSMS to search for, I chose “The server…”. You can play around later to see what the options do if you like, these selections are not remembered so once you close the window they go away. After clicking OK you will see your instance name show up under Securables and the bottom pain will show all the instance level permissions. I scroll all the way to the bottom and will see the permissions I assigned to my login:

![](/images/securables_showing_thumb.jpg)

That is all for now…