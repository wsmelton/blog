---
title: Calc-MaxSample
date: 2013-11-13T10:00:00-06:00
draft: false
tags: [powershell]
---

I am working on building a function that will allow me to gather performance counter data across multiple servers. I knew this had done by someone in the SQL Server family and went to search the inter-web. I came across Aaron Bertrand’s (<a href="http://sqlblog.com/blogs/aaron_bertrand/default.aspx" target="_blank">blog</a> `|` <a href="http://twitter.com/AaronBertrand" target="_blank">twitter</a>) blog post <a href="http://sqlblog.com/blogs/aaron_bertrand/archive/2011/01/31/how-i-use-powershell-to-collect-performance-counter-data.aspx" target="_blank">here</a>.

This gave me a starting point, however I also noticed that with the use of the basic <a href="http://technet.microsoft.com/en-us/library/dd367892.aspx" target="_blank">Get-Counter</a> cmdlet you provide the –MaxSamples value to tell PowerShell how long you want to collect counter information.

You would want to calculate this based on the –SampleInterval value. A few examples of this can be found in the comments on Aaron’s blog post. If you want to cover a 2 hour period and get a sample every 30 seconds, you would set MaxSamples to 240.

This is a mathematical equation that I did not want to have to keep doing every time. So I decided to build a small function that I added to my PowerShell ISE profile. I don’t use the the console all that much anymore with PowerShell 4.0. The below function includes a bit of help information as well. So, once you load this function into the console or your profile you can use Get-Help cmdlet if needed.

```powershell
<#
.Synopsis
  Assist calculating the max sample for Get-Counter
.DESCRIPTION
  Calculates from the sampling value and the hours desired what the max sample value should be for the Get-Counter cmdlet
.EXAMPLE
  Cal-MaxSample -secSample 15 -hours 3
   This example based on the SampleInterval and the number of hours desired output what the MaxSample value should be
.PARAMETER secSample
    The SampleInterval value to be used in Get-Counter command, Int32 value between 2 - 60. The default value for
   Get-Counter command is 1 (one)
.PARAMETER hours
   The number of hours desired for capturing performance counter data with Get-Counter command
#>
function Calc-MaxSample
{
   [CmdletBinding()]
    [OutputType([int])]
   Param
    (
       [Parameter(Mandatory=$true,
                   Position=0)]
       [ValidateRange(2,60)]
        [int32]
       $secSample,
       [Parameter(Mandatory=$true,
                    Position=1)]
       [int]
        $hours
   )
   [int]$calValue = (($hours * 60) * 60) / $secSample
   Write-Host "Based on following calculation: (($hours * 60) * 60) / $secSample)" -ForegroundColor Yellow -BackgroundColor Red
    Write-Host "MaxSample value = $calValue" -ForegroundColor Yellow -BackgroundColor DarkGray
}
```
