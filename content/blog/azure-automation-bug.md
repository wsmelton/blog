---
title: "Azure Automation Bug"
aliases: [/azure-automation-bug/]
date: 2018-08-10T15:10:52-05:00
tags: [azure]
---

Long time, no post...

I have recently changed positions at Pythian and now work on projects full time. My current project has lead me down the road of finally getting to dig into Azure more. This particular project, I am working on automating SQL Server builds from the point of "new VM", push the button and it installs and configures SQL Server to cover various scenarios for the client.

Being that it is Azure Automation I am opted to use the [AzureRm](https://powershellgallery.com/packages/azurerm) module as much as I can. I have been going back and forth trying to figure out a few things around Azure DSC and configurations I am writing for the project. When I happened upon a bug in the AzureRm module.

I have already submitted an issue to the repository for this [here](https://github.com/Azure/azure-powershell/issues/6899). The gist is the `Import-AzureRmDscConfiguration` is not validating the characters in the configuration name itself. Which causes you to have false hopes 😞.

When you go to delete the configuration via the portal you get a lovely error that actually tells you it is an invalid name and cannot complete the operation. The only way to drop it is to use the PowerShell command `Remove-AzureRmDscConfiguration`.

The irony of all this is you can sit there thinking everything is hunky dory and being wondering for days why hitting the compile button in the portal does not work. You can also run `Start-AzureRmDscCompilationJob` until you are blue or dead from starvation because it runs and completes the compilation, but does not output anything or give any error.

Just a heads up until that is fixed on the module side....hopefully you didn't spend a few days wondering why the configurations were not working. Not saying I did of course it was just one or two days of my time 🌧️.