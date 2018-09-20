---
title: CTRL plus ALT plus what?
date: 2014-09-15T08:00:00-06:00
drafts: false
tags: [powershell]
---

Depending on how far back you go in the technology field you all remember having to use CTRL+ALT+DELETE to change your password for your domain account.

![](/img/change_password.png)

Well, I always remote into servers now a days with consulting for various clients. I never like to keep the password assigned and generally will attempt to change it using PowerShell:

```powershell
$cn = gpresult /R | Where {$_ -match "CN"} | Select -Skip 1 | clip
$acct = [adsi]"LDAP://$cn"
$acct.psbase.invoke("SetPassword","MyNewPassword")
$acct.psbase.CommitChanges()
```

Most of the time though I get access denied so how can you change it over VPN, when your machine is not part of their domain? Well starting in Windows Server 2008 (I think) Microsoft added a new key sequence that acts like CTR+ALT+DELETE for that machine.

You can now execute CTRL+ALT+END to get to the prompt to change your password. On Window Server 2012 it looks similar to this:

![](/img/change_password2.png)

Click on "Change a password" and you get the similar prompt to the older versions of Windows:

![](/img/change_password3.png)
