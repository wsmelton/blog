---
title: "A Dash of Azure Data Studio"
date: 2019-03-13T17:00:00-05:00
publishdate: 2019-03-13
lastmod: 2019-03-13
draft: false
tags: [azuredatastudio]
---

_If you are not familiar with Azure Data Studio (ADS) please check out my previous post on [Azure Data Studio - User Interface](/ads-userinterface/)._

## Visualize

The power of ADS offers the ability to use extensions that offer visual insights and functionality via dashboards, or customize it yourself creating [custom insight widgets](https://docs.microsoft.com/en-us/sql/azure-data-studio/tutorial-build-custom-insight-sql-server?view=sql-server-2017). A good portion of extensions offerred as of this writing are insight dashboards, where they offer up information of various areas. A dashboard usually has two layers:

1. Overview visual (graphs, pretty pictures)
1. Detail visual (generally list format)

Others will offer things like being able to script an item or create an item (e.g. databases). In this post though I'm going to focus on the insight dashboards as they seem to be most common of the extensions I've seen so far.

## Overview Visual

I'm going to use the Home tab from the Manage dashboard in ADS as it is built-in to ADS and illustrates the most common functionality you will find going forward.

![](/img/ads_dash_visual.png)

In the above you can see the static information across the top ("Server Dashboard"). You have the option to refresh this information in the menu list. The next section offers more interaction. You can open the menu on the "Database Size" graph and see you can `Run Query` or `Refresh`.

![](/img/ads_dash_visual_1.png)

Refresh, is exactly what you would think and simply updates the current visual (e.g if you have added database you would see it listed). _It is worth noting that the data in the dashboards will not refresh automatically._

The `Run Query` will open a new query editor and populate it with the query used to pull the data for that visual. It will automatically execute it once the query window makes a connection:

![](/img/ads_dash_visual_2.png)

## Details

If you we look at the Backup Status menu we can see an additional option: `Show Details`:

![](/img/ads_dash_visual_3.png)

Clicking on that a pop-out side bar will show up on the right:

![](/img/ads_dash_visual_4.png)

In additional to showing the row-level details of each database identified you also have the option to open the backup task (by clicking on "Backup") for a database listed. _The Backup task is a built-in feature of ADS._

## Preview Extensions

One thing of importance is there are a number of extensions from Microsoft (at the time of this writing) that you will are noted as being in preview.

![](/img/ads_dash_preview_extension.png)

This is associated with a preview setting in ADS that you have to enable in order to use them. You go into your settings, you have two options to access your settings:

- Use the sprocket on the bottom of the Activity Bar, then click on "User Settings"
- `CTRL + SHIFT P` to bring up the command palette, type `users` and select the `Preferences: Open User Settings`

You can search for `preview features` and then simply ensure this is checked:

![](/img/ads_dash_preview.png)

If you operate via the `settings.json` file you will want to add this entry:

```
"workbench.enablePreviewFeatures": true
```

You can see with this setting enabled (set to true) I have the options for `SQL Agent`, `Server Reports` and `whoisactive` showing:

![](/img/ads_dash_preview_enabled.png)

When it is disabled I loose those tabs:

![](/img/ads_dash_preview_disabled.png)

## Additional Help

If you find any issues with ADS you can submit issues to their repository [https://github.com/microsoft/azuredatastudio/issues](https://github.com/microsoft/azuredatastudio/issues). If you find issues with any extensions that are not authored by Microsoft you will need to submit an issue to that author's repository. Sadly at the time of this writing a good bit of them do not provide information in the extension details, when you view them in ADS. You can take the name and simply search on GitHub or clicking on the "Install" at this time would be the quickest way to get to their repository on GitHub. (Maybe Microsoft will enforce more information being included down the road).