---
title: Dynamically Build RDP Files
date: 2015-10-26T08:00:00-06:00
drafts: false
tags: [powershell]
---

_This post was originally published 26 July 2011, updated the script and the post since I have learned a good bit on PowerShell since the original post._

I was pretty excited that work was finally going to install <a href="http://www.microsoft.com/download/en/details.aspx?id=21101" target="_blank">Remote Desktop Connection Manager v2.2</a> on our laptops, until I started using it. It is nice if you work on one server at a time but sometimes I multitask while something is running, or I need to compare something to the results on another server. You can “undock” the window and then go to full screen like you would with the regular Remote Desktop Connection, however you have to do that for each server and each time after closing it.

So I decided to go back to RDP files, using Remote Desktop Connection. I did not want to go through the process of having to create those files all over again. So I wanted to see if PowerShell could do it for me.

A quick search on Google I came across a post from the Windows PowerShell Blog on <a href="http://blogs.msdn.com/b/powershell/archive/2008/09/14/rdp-file-generation-use-of-here-strings.aspx" target="_blank">RDP file generation</a>. The post is actually a review of a script someone wrote and blogged about that will <a href="http://everydaynerd.com/microsoft/create-multiple-rdp-files-with-powershell" target="_blank">create multiple RDP files with PowerShell</a>.

I decided to start with this, but do a few things differently. As mentioned in the blog post, a flaw in the original script is a hard coded CSV file. I updated this to be more dynamic in the sense that you pass in the server name as a string array, or pipe it to this command/script. As well, new version of the script assumes the current directory, so where you run the script from is where the files will be created. I did not care about creating directories, or creating RDP file with different resolution settings.

I have updated the script with help syntax so you can just view that via the `Get-Help` cmdlet. There are 3 parameters, which 2 are required and one is optional.

For the "default" or RDP template file I just opened up Remote Desktop Connection (Windows Key + R &gt; mstsc.exe). Go through it and just set it to your preferences (Display, Local Resources, etc.). Then under the General tab click “Save As…”. Save the file to your preferred location and remember this is the path you will pass into the script. Then using Notepad open that file up and you will see something similar to this:

![](/img/mydefault_thumb.jpg)

The highlighted line is what you want to remove and then save the file. This line will be added by the script and include the server name passed into the parameter of the script.

```powershell
function new-rdp {
    param(
        [Parameter(Position=0,Mandatory=$true)]
        [string]$server,
        [Parameter(Position=1,Mandatory=$false)]
        [string]$MyDefaultRDP = '\\ottprodfs01\vdi\melton\Documents',
        [Parameter(Position=3,Mandatory=$false)]
        [string]$fullpath = '\\ottprodfs01\vdi\melton\Documents\Remotes'
        )

    ForEach($entry in $server)
    {
        $entry
        #build the file
        $filename = $fullpath + $entry + ".rdp"

        #add hostname and username /if provided/ to rdp file

        # Add hostname in RDP file
        $temp = "`nfull address:s:" + $Entry

        #check to see if file exist
        if (Test-Path $filename) {
            Remove-Item $filename -force
            Write-Host "Found $filename was already there, so I deleted it for you" -Foregroundcolor Red }
        else {
            $temp | Out-File $filename
        }
        Get-Content $MyDefaultRDP | Out-File $filename -Append
        Write-Host "$filename created"
    }
}
```
