---
title: "Azure Data Studio User Interface"
date: 2019-03-10T00:19:31-06:00
draft: false
notoc: falses
---

## Short intro
In September of 2018, Microsoft brought us Azure Data Studio (ADS). This is a cross-platform tool for querying and managing data development. It is meant to compliment SQL Server Management Studio (SSMS) but for those that do not wish to work on Windows it can be a tool of choice for connecting to both SQL Server and Azure SQL DB.

ADS itself was built using [Visual Studio Code](https://aka.ms/vscode) (Code) as the base and then Microsoft built upon that to what we have today. If you are not familiar with Code or have never used it it can be a bit daunting to get around. The purpose of this post is to give you a starting point and map (of sorts) on how to get around and start using it.

## Release Channels

Code has two build streams and as such ADS has followed the same suite. So when you prepare to deploy this tool for your team (or yourself) you can choose between two "channels" (as they are called):

- [Stable Build](https://docs.microsoft.com/en-us/sql/azure-data-studio/download)
- [Insiders Build](https://github.com/Microsoft/azuredatastudio#azure-data-studio)

_Check the list of links in the readme for the insider installation based on your OS preference._

The Stable Build would be considered the general available (GA) release of ADS. It is a production ready version of the software; while the Insiders Build is pre-release and understood that bugs may (and will) be introduced with each release of the software. Now one thing to note is the while the stable release is considered production ready, that does not mean it won't come with some bugs as you use it in your particular environment.

## Extense and Extensibility

The power that comes with ADS being based on Code is the ability to extend it via extensions. You can have an extension that offers additional data views, formatting queries or search a database for particular object or text string (e.g. RedGate SQL Search).

I would say the most common extension you will find useful will be the ones that provide Dashboard Insights. These allow you to visualize data in various ways and more easily access the information. These are similar in nature to the "Reports" that came backed into SSMS.

## Report Bugs, Issues or Feature Request

First and foremost it should be understood that ADS is an open source project that Microsoft maintains and host. As such, bugs and issues you find cannot be fixed if Microsoft does not know about them. They are very keen on getting things fixed for you and the same goes for feature request. In the help menu of ADS you will find an option "Report Issue" that offers a simple form to fill out with the details of what you found or want.

![](/img/ads_reportissue.png)

You can find a bit more detail on submitting bugs and suggestions on their wiki [here](https://github.com/Microsoft/azuredatastudio/wiki/Submitting-Bugs-and-Suggestions).

## Basic lay of the land

This is a common view of ADS (as of this writing):

![](/img/ads_basicui.png)

Let's just go left to right on this screenshot:

1. Activity Bar - You can switch between views of the side bar and gives you additional context-specific indicators or content. (More on this later on...)
1. Side Bar - Based on the currently active view but in general will be additional data or items to interact with in some fashion (e.g. file list)
1. Status Bar - Information on current files or projects you have opened. The information will change based on the editor you have in focus.
1. Panels - The 3 that are included right now are not all really utilized at the time of writing. The "Problems" panel is associated with displaying information related to editors that you may have open. The example in the screenshot shows syntax errors for the query window I have open.
1. Editor Groups - The main area where you will do your work. The example shows I have two editors open. The left is what is referred to as an "Insights Dashboard". The right is just a new query editor where I have executed a basic T-SQL statement.
1. Query Output Options - This is where the power comes in for the query editor in ADS. You have the ability to chart a given dataset returned by your query. You can also output the data to JSON, CSV, XML or export it directly into an Excel file (does not have to be installed).

## Activity Bar

### Servers

The first side bar you interact with is Servers, you can quickly focus this side bar using the keystroke `CTRL + G`. Upon making a successful connection to a given Azure SQL or SQL Server instance you will be presented with this view:

![](/img/ads_activitybar_servers.png)

This side bar gives you the folder view of the databases, security and server objects. You can do a bit of organizing for your servers (if you need to work with multiple). If you worked with Local Groups in SSMS you will be familiar with this feature.

![](/img/ads_activitybar_servers_icons.png)

Clicking on "New Group" you are presented with the dialog to name the group, add a description and pick a color for it:

![](/img/ads_activitybar_servers_newgroup.png)

Once added you can see it shows up in the Servers side bar, and you can actually just drag the server name down onto the "Local" and it will organize that instance to that group, on the fly.

![](/img/ads_activitybar_servers_localgroup.png)

One added bonus is as you add groups they also show up in the connection dialog. This allows you to add a server directly to the group on first connection.

![](/img/ads_activitybar_servers_newconnection.png)

### Task History

This side bar can be accessed using the `CTRL + T` keystroke. The purpose of this side bar is to view progress status of backups and restores, down the road it may hold progress status for other task as well.

![](/img/ads_activitybar_taskhistory.png)

Once you run a restore or backup you will then see a list of the status whether it was successful or failed. You can double-click on a given failure to see the full context of the error message.

![](/img/ads_activitybar_taskhistory_failure1.png)

Which as of this writing the error for a failed backup only displays a generic one. I have [submitted a feature request](https://github.com/Microsoft/azuredatastudio/issues/4397) to have this error be more descriptive on the actual issue than a generic one.

![](/img/ads_activitybar_taskhistory_failure2.png)