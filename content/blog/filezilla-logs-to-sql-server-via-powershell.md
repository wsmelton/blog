---
title: FileZilla Logs to SQL Server via PowerShell
date: 2014-12-01T08:00:00-06:00
drafts: false
tags: [powershell,sqlserver]
---

I had a client that uses FileZilla for FTP, where little files are constantly being sent to this server from numerous devices. In this situation I needed to be able to have it log those connections so I could try and track down an issue. [I'm a man with many hats.] So I went into FileZilla Server Interface and enabled logs to be created by day. I thought I might be able to just parse them easily with PowerShell, but yeah not really.

Through a bit of searching I found a few articles that talked about how ugly the logs for FileZilla actually are and <a href="http://strivinglife.com/words/Post/Parse-FileZilla-Server-logs-with-Log-Parser" target="_blank">found one that utilized LogParser</a> to change them into W3C formatted files. Which I decided to go a step further and just put them into a SQL Server table.

My intention was to have a SQL Agent job, with a PowerShell step, that would look at the log file directory and import the log for that day into a table created for that day. _I am not fond of putting dates into a table name, but in this situation I did not particularly want to put much effort into setting this up._ I spent an hour or so troubleshooting what turned out to be this "log_2014-11-14" needed to actually be "[log_2014-11-14]" (with the brackets) in the query for LogParser, mostly because of the stupid error message being returned in PowerShell.

The complete code I use in the job step is below. I have had this running for a few days now and it works well enough. I then just went through and created a few procedures to pull out the information I wanted, using a parameter to just pass in the date of the table I wanted to pull.

You can find the complete script [here](https://gist.github.com/wshawnmelton/ee4ef5f489a8867169c7).
