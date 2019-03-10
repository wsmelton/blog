---
title: What OS permissions does SQL Server have?
date: 2011-04-28T09:00:00-06:00
draft: false
---

If you set the service account for the SQL Server services up at installation you are ahead of the game when dealing with securing your SQL Server installation. However there are some environments where the DBA does not do the initial installation of SQL Server. That requires the DBA to go back and configure a custom account for the services after the installation.

In most instances if you use the SQL Server Configuration Manager (SSCM) to set the service account it should configure all the file, registry, and operating system permissions SQL Server needs for you. See this <a href="http://technet.microsoft.com/en-us/library/ms174212.aspx" target="_blank">TechNet article on SSCM</a>.

A question to ask is do you ever go back and periodically check to see what operating system permission the account was actually given? Do you check to make sure someone has not dorked around with the permissions and made your SQL Server instance not come back up at next reboot?

Well you can do this by opening up the group policy editor on the server and go through each <a href="http://msdn.microsoft.com/en-us/library/ms143504.aspx" target="_blank">permission SQL Server is supposed to have</a>. However, you would have to go through all of the OS permissions to make sure the service account has not been granted excessive permissions to the operating system.

Well who wants to use the GUI when we can use PowerShell!!! So here is a nice little one-liner I use to verify what permissions the SQL Server service account(s) have on a server:

`Get-WMIObject -Namespace root\rsop\computer -Class RSOP_UserPrivilegeRight -Recurse |
Where-Object {$_.AccountList -like "*SQL*"} | Format-Table UserRight -AutoSize`

This portion of the code is where you will adjust it for your environment: `{$_.AccountList -like "*SQL*"}`. As written above this will return the permissions found to have an account name/group assigned to it that contains the text "SQL" within the name. Adjust this portion to your specific requirements.

This is a screenshot of what your output should resemble. (Do you see the excessive or un-needed privilege returned in the output?):

![](/images/results.jpg)

**_A little bit of a caveat for you on this code though is that it will only work on domain member servers. For some reason, that I never bothered to look up, the RSOP namespace is not available or accessible on stand-alone servers._**
