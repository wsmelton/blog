---
title: Adjusting and learning
date: 2011-08-18T08:00:00-06:00
draft: false
---

Short and sweet post here...not the sugar sweet, the awesome sweet!!!

So I'm still working on the script I talked about in a <a href="/2011-08-01-what-a-few-lines-of-code-can-do" target="_blank">previous post</a>. I wanted to try to drop using the parameter and try to work it all out in the script if it comes across more than one instance.

So I came up with this, initially:

```powershell
$regInstance = (Get-ItemProperty 'HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server').InstalledInstances
if ($regInstance.Count -gt 1)
{
   "More than one instance found on server."
   foreach ($ins in $regInstance)
   {
     $regPath = (Get-ItemProperty 'HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\Instance Names\SQL').$ins
     $fullpath = "HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\$regpath"
   }
}
else
{
   $regPath = (Get-ItemProperty 'HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\Instance Names\SQL').$ins
   $fullpath = "HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\$regpath"
}
```

So that was nice, but you probably already noticed an issue? The way it is written the `$fullpath` will only have the last value it hits in the foreach loop, if more than one SQL instance exist. That will not work. So where do we turn...hash tables. How you might ask? While we pause for station identification, go read this <a href="http://blogs.technet.com/b/heyscriptingguy/archive/2011/07/05/automatically-create-a-powershell-hash-table.aspx" target="_blank">post</a> from The Scripting Guy! Blog.

The example in that post that helped me was adding 100 intergers as key/value pairs in a hash table. I could capture both the InstalledInstances and the Instance Names values, and keep them associated with each other  in a hash table. This improves the options I have of reusing this snippet in other scripts possibly. (One example comes to mind is being able to pass the instance name in SMO scripts.)

So the 18 lines of code from above, turned into this:

```powershell
#create hash table
$hashInst = @{}
#populate hash table with values
$inst = (Get-ItemProperty 'HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server').InstalledInstances
foreach ($i in $inst)
{
   $hashInst.Add($i,(Get-ItemProperty 'HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\Instance Names\SQL').$i)
}
```

A total of just 6 lines of code for readability, could go down to 3 if you put the foreach on one line.
