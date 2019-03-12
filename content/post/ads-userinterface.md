---
title: "Azure Data Studio User Interface"
date: 2019-03-11T12:00:00-06:00
draft: false
---

> Warning: This post is long but if you want to get familiar with Azure Data Studio as a first time user, hopefully it will be a good read for you.

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

### Explorer

Access using `CTRL + SHIFT + E`. This side bar is only active (or usable) when you have opened up a workspace (aka "folder").

![](/img/ads_activitybar_explorer.png)

### Search

Access using `CTRL + SHIFT + F`. This one is only usable when you have a workspace open. It allows you to search and do the find/replace against files you have in the workspace.

![](/img/ads_activitybar_search.png)

### Source Control

Access using `CTRL + SHIFT + G`. If you have a workspace open that has been initialized as a Git repository (or other source provider) then it will display various options for you to commit, stash, stage, add a comment message, etc. In the example screenshot I have a GitHub repository open from my local machine:

![](/img/ads_activitybar_sourcecontrol.png)

### Extensions

Access using `CTRL + SHIFT + X`. This will be something you want to keep an eye on as time goes to find out what new extensions have been released by Microsoft and the community. The main ability of ADS is being able to extend it using extensions. Just go through and explorer this list when you have time; install one and give it a try (on a test instance obviously).

![](/img/ads_activitybar_extensions.png)

### Azure

There is no shortcut key to access this one. Extensions that will support an activity bar item do not always include a shortcut keybinding. I'm going to spend a bit more time on this one as it requires a bit of setup to use. This revolves around access an Azure subscription and the Azure SQL service.

![](/img/ads_activitybar_azure1.png)

The following illustrates the steps needed to add your Azure account to ADS.

![](/img/ads_activitybar_azure_addaccount.png)

After a few seconds, you will have access to any subscription and Azure SQL resources your login has access to:

![](/img/ads_activitybar_azure_account.png)

Now you may wonder what all does this allow you to do or help you with? Basically just saves you the hassle of having to save all those connections and remembering what the full server name is for that new Azure SQL DB that was just deployed. When you put your mouse/cursor on a given server or database you will see a connect icon. Clicking on it will open the Connection dialog and have the Server and Database auto-populated for you.

![](/img/ads_activitybar_azure_connecticon.png)

![](/img/ads_activitybar_azure_connection.png)

The above you can see the server name and database were populated. Since I chose a server it uses master database, if you choose a database though that given database would be placed in the box. (_It defaults to use `dbadmin` for the login no matter what server or database I selected._)

## Extensions

I want to circle back around to this one as it will vary how you actually get a given extension installed. The extensions that Microsoft published will just need you to click on that install button, and ADS will install it for you. The extensions that come from the community or vendors will tend to send you to GitHub repository.

![](/img/ads_extensions_frk.png)

When you click on the install you are taken to the release page on GitHub, which you will then need to download the vsix file on that page:

![](/img/ads_extensions_frk_github.png)

Then go back into ADS, under the extensions side bar you will click on the 3 dots and click on `Install from VSIX...`

![](/img/ads_extensions_frk_addvsix.png)

After that you will be prompted to browse to where you saved that file from GitHub. Then just click on the "Install" button, and since this particular one is a 3rd party (non-Microsoft item) you will get a security warning to click yes or no. If you chose to click yes you, after it installs, you will receive a prompt to `reload now`. ADS has to restart for any new extension to become active.

## Additional help

If you are looking to ask any more questions around using ADS, bugs you found or questions about documentation....or you just want to chat about Azure Data Studio you can come chat it up in SQLCommunity Slack channel. You will find us under `#azure-data-studio` and Microsoft is involved in this channel as well. You will commonly find Alan Yu checking in often during the day (he is one of the PMs over ADS).