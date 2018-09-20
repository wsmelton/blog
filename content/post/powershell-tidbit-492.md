---
title: PowerShell Tidbit #492
date: 2013-11-05T08:00:00-06:00
draft: false
---

I do remote support work now as a DBA and have clients that provide my password for VPN login or Active Directory login. I usually access their network through a central remote server that I will use to manage their SQL Server environment. As some of you may know there is no way to change your password through remote desktop until it expires and prompts you to upon login. Depending on the version of Active Directory they are running you may get a little bubble down by the clock that you can use as well, but I tend to miss that most of the time.

So I wanted an alternative so I could change it when I needed to, as some clients do not have as strict a policy regarding password changes as I would like. I took the web and came across a nice post by the Scripting Guys <a href="http://blogs.technet.com/b/heyscriptingguy/archive/2010/08/17/how-to-change-a-user-s-active-directory-password-with-powershell.aspx" target="_blank">here</a>.

I was not really interested in using this as a function, just needed the commands to use. This article has the exact thing you need so go read it…

The one thing I needed to add was knowing the full AD path of my user account. You all know what yours is right?

Well you can use `gpresult /R` to get that information. All I did was put a bit of PowerShell flare into it. If you are not familiar with the results of this command go ahead and issue it on your computer, if you are part of a domain. It will give you the domain information about the computer and your current login. I like looking at this every so often to check the policies that are applied in the domain.

Anyway there are two AD paths that are returned with this command, I only want the second one. It always returns the computer account first and then your login. So this command provides me that and puts in the clipboard for me:

```powershell
gpresult /R | Where {$_ -match "CN="} | select -Skip 1 | clip
```

Combine this with the commands from the article:

```powershell
$acct = [adsi]"LDAP://<paste result here>"
$acct.psbase.invoke("SetPassword","MyNewPassword")
$acct.psbase.CommitChanges()
```

You may normally see me write functions for this, but for this particular area I like to see it as it works, just to be safe. You may also see the “invoke” command take a while on some domains, just depends on the architecture I guess.

Once you hit enter on the CommitChanges command your password has been updated.