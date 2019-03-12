---
title: "Check-InstanceConfig (part 2)"
date: 2013-12-09T09:00:00-06:00
drafts: false
tags: [powershell,sqlserver]
---

In the <a href="/2013-12-04-ps-check-instanceconfig-part-1" target="_blank">previous post</a> I discussed the data table that holds the default values for the configuration options in SQL Server 2000 up to SQL Server 2014.

In this post I will go over the function(s) that are included in the script. I will keep the same format as I did in the previous post:

- How it was written
- What it contains
- A few examples

### How it was written

If you have already downloaded the script you notice it had one function. I was attempting to make the output similar to what Mike did in his T-SQL script with the text output. After looking at it a bit more and thinking on best practices for PowerShell, I chose a different route. I always try to ensure whatever my functions output, you can do something with them down the pipeline. In order to keep that going I opted to break this up into separate functions. I also included a function that allows you to just pull the raw configuration options from the instance as you wish.

### What it contains

There are 4 functions included in the current version of the script:

- Pull-SqlConfig – Just pull the configuration options information on the instance
- Check-SqlRunConfig – Compare the running value to the configured value
- Check-SqlRunDefault – Compare the running value to the default value
- Check-SqlBadDefaults – Compare the running value to the default value for specific options.

I decided to also include help text with each function so loading the script into your PowerShell session you can simply use the Get-Help cmdlet and it will show you the information on each function. Adding the `-full` switch to the command will output more detailed information as well.

![](/img/check_instances_p2_1.png)

### A few examples

As mentioned above the function help information also includes a few examples of each function. So if you want to see them you can simply use the Get-Help function along with the `–Examples` switch.

![](/img/check_instances_p2_2.png)

Here is the <a href="https://github.com/wsmelton/scripts/blob/master/posh/Check-InstanceConfig.ps1" target="_blank">full script</a>. This link will always point to the current version of the script. My next blog post will explain the function in the script.
