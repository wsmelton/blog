---
title: Counting the Days in PowerShell
date: 2020-09-11T08:00:00-06:00
draft: false
---

At times you need to figure out various ways to count the days for a script. In some cases you may need to do things like:

- How many days are in the month
- What is the last day of the month
- How many work days are in the month

There are various reasons for knowing the answers to the above, but they are always questions I have to look up how to do them in PowerShell. So this post is more of a cheat sheet for me, but you are welcome to take a copy of it if you want or need it.

Now most common way to get the date in PowerShell is to utilize `Get-Date` in various ways. However, you will see below there are some cases we have to revert to good 'ole .NET classes.

### Days In The Month

Syntax:

```
[DateTime]::DaysInMonth( <year>, <month> )
```

The values passed into this method have to be the numeric value. The way you can make this dynamic for your code is to grab the current year and month using `Get-Date`, like so:

```powershell
[DateTime]::DaysInMonth( (Get-Date).Year, (Get-Date).Month )
```

### Last Day of the Month

This requires you to simply utilize the above to first grab the number of days in the month, and use `Get-Date`.

```powershell
$DaysInMonth = [DateTime]::DaysInMonth( (Get-Date).Year, (Get-Date).Month )

```