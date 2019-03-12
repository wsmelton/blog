---
title: "Github Issue Templates"
date: 2018-05-13T20:00:00-06:00
draft: false
tags: [dbatools]
---

Who has not heard of [GitHub](https://github.com) yet? For those embarrassed to raise your hand, it is simply a hosting service for version control and offers free subscriptions along with paid (allows private repositories and such). It has become common place for PowerShell modules and the like to be hosted on GitHub. Microsoft has moved a number of projects and products to GitHub, big one being [PowerShell](https://github.com/powershell).

The benefit you can have hosting your project on GitHub is it includes a bug report system and workflow. The users can come by the repository on GitHub and submit issues from anything between a bug report to a feature request. Some repositories also utilize this workflow for support, to a small degree.

I happen to be a maintainer for the [dbatools](https://dbatools.io) PowerShell module. The module is available from the PowerShell Gallery but the code itself is developed and managed on GitHub.

## New Template UI

GitHub posted on their [changelog](https://blog.github.com/changelog/) at the start of May that they have added "[Multiple template choices](https://blog.github.com/changelog/2018-05-02-mutiple-template-choice/)". Prior to this you only had an option to create one issue template. So if you wanted users different types of information based on a bug report or feature request, you had to add all the information in sections. You can see an example of this with the [old issue template](https://github.com/sqlcollaborative/dbatools/commit/80d95e7d556ebc9bc9c0ba59af2f69592b16e522#diff-01777e4a9846fea5f3fcc8fe40d44680) we had with dbatools project.

We now have multiple template options to chose from based on your need or issue. Now when you go to our [issues](https://github.com/sqlcollaborative/dbatools/issues) and click on the "New Issue" button you are taken to a page that gives you [choices](https://github.com/sqlcollaborative/dbatools/issues/new/choose):

![](/img/github_issue_choose.png)

## Setup

_Do note you will have to be an admin in the repository to perform these steps._

To get started with this it takes just one or two steps:

* Go to the Settings of the repository

![](/img/github_issue_settings.png)

* Under the "Features" section you will see a button  "Set up templates", click on that button.

![](/img/github_issue_settings_2.png)

* You are now presented with a screen that shows no templates created.

![](/img/github_issue_settings_3.png)

* You can select the drop down

![](/img/github_issue_settings_4.png)

* The two canned templates included are for bug and feature request.
* Add each one and then you will see an option to "Preview and Edit"

![](/img/github_issue_settings_5.png)

* From there you can an option to do 3 things:

![](/img/github_issue_settings_6.png)

1. Close the preview
2. Delete the template
3. Edit the template

You can see out-of-the-box that they provide a very good template, but you are free to edit to your required information desired.

Once you have all those templates added and edited, you will need to use the "Propose changes" button on the top right to commit the changes. Clicking on that button simply provides the usual form to commit changes to the repository:

![](/img/github_issues_settings_7.png)

> NOTE: The templates have to be committed to the default branch of the repository in order for them to be accessed/usable.

Once you commit and merge the changes you will find the templates are created under the following directory of the repository: `.github\ISSUE_TEMPLATES`.

![](/img/github_issues_settings_8.png)

## Reminder

Obviously this is a new feature on GitHub, but the only bug I have found is if you edit a custom template outside of the interface/process I noted above it disappears from the choose prompt. I am not sure why and have not found any reports of this yet.

But do just note that if you want to edit the templates it is best to go through the Settings > Set up templates workflow.