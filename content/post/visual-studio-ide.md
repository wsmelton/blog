---
title: Visual Studio Community
aliases: [/vs-community/]
date: 2018-01-04T19:35:00-06:00
draft: false
---

I have typed a good bit in the past year evangelizing about Visual Studio Code on social media and other forms. As a major contributor for the PowerShell module <a href="https://dbatools.io" target="blank">dbatools</a> I have made VS Code my primary development tool. You may not know that I actually started out using the big brother Visual Studio 2015 Community Edition ("VS") before I found VS Code. VS, now at version 2017, and the <a href="https://marketplace.visualstudio.com/items?itemName=AdamRDriscoll.PowerShellToolsforVisualStudio2017-18561" target="_blank">PowerShell Tools for Visual Studio</a> have come a long way since I last used them. The PowerShell extension in VS is maintained by <a href="https://github.com/adamdriscoll/poshtools" target="_blank">Adam Driscoll</a>. In this post, I thought I would take you through getting VS 2017 installed and setup for PowerShell development. I will go over how to get VS setup for contributing to a GitHub project. _We will obviously use dbatools as the example repository._

<!-- TOC -->

- [Install](#install)
- [Extensions](#extensions)
- [Versions](#versions)
- [VS - Solutions, Projects and now Folders](#vs---solutions-projects-and-now-folders)
- [Starting New](#starting-new)
- [Starting From Current GitHub Project](#starting-from-current-github-project)
    - [Cloning the Repository](#cloning-the-repository)
- [Caveats with PowerShell Projects](#caveats-with-powershell-projects)

<!-- /TOC -->

### Install

The first step is to download the installer from [here](https://visualstudio.com/free-developer-offers). You will also need to [download Git for Windows](https://git-scm.com/download/win) on your machine. The install for Git is very basic (just click next), so I will not go over that installation. I will walk through the installation of Visual Studio 2017 Community Edition below showing the screenshots in the order I received:

![](/images/vs-install_1.png)

Click continue

![](/images/vs-install_2.png)

At this point, you are prompted to select a workload and individual components. You can go through and select the ones you desire, but I am opting to skip this process right now. (Adding more workloads does add on time for the install process).

![](/images/vs-install_3.png)

You will get a screen showing the installation progress (VS updates will also have this same prompt now as well):

![](/images/vs-install_4.png)

Once that is completed you can click on "Launch" button:

![](/images/vs-install_5.png)

One final step before VS opens is to [sign in with your Live account](https://msdn.microsoft.com/en-us/library/dn457348.aspx#Anchor_0).

![](/images/vs-install_6.png)

![](/images/vs-install_7.png)

You should now be presented with something similar to this:

![](/images/vs-install_8.png)

### Extensions

Now that we have VS installed we will need to add the PowerShell extension. Start by going to Tools > Extensions and Updates...

![](/images/vs-install_9.png)

1. Select "Online"
2. Search for "PowerShell"
3. Select "PowerShell Tools for Visual Studio"
4. Click Download

![](/images/vs-install_10.png)

Once that download completes you can close that window, and then exit out of Visual Studio. It will vary but after a few seconds, you will see the VSIX Installer open up and begin installing the extensions.

It will first initialize and then give you a prompt to click "Modify" for the install to continue:

![](/images/vs-install_12.png)

![](/images/vs-install_13.png)

On my machine, the install of the PowerShell extension took close to a full hour. Once the extension install is complete, just click "Close":

![](/images/vs-install_14.png)

### Versions

The remainder of this post and screenshots will focus on the following versions of VS and PowerShell extension on my machine:

- Visual Studio Community 2017 - 15.5.1
- PowerShell Tools for VS - 3.0.585

### VS - Solutions, Projects and now Folders

If you have used SSDT with the Business Intelligence projects you may be familiar with Visual Studio's use of [solutions and projects](https://docs.microsoft.com/en-us/visualstudio/ide/solutions-and-projects-in-visual-studio) to organize things. This was the core configuration of how you worked in VS. As times have changed so has VS and in VS 2015 release they added support for using a root folder as your solution. So you can now open a PowerShell module root folder as a solution in VS. Which if you have used VS Code this works the same way. A reason for adding the folder support was because of GitHub, which a high majority of PowerShell projects on GitHub will not include the VS solution and project files.

There is a downside to the folder support in VS: No project template is associated with it. What that means is you can open a PowerShell module in VS as easily as just pointing it at the root folder of your module, but you will not get all the bells and whistles that PowerShell Tools for VS includes. I have not found a clean way of just "importing" a PowerShell module from GitHub into a PowerShell Tools project in VS, so the steps I will show you later may seem a bit wonky but it is the only way I've found that works.

### Starting New

If you are developing a brand new PowerShell module, you simply use the PowerShell Module project template. You can do this via File > New > Project, then select the template and give it a name.

![](/images/vs-install_15.png)

This will create a very basic module file structure. You can check the box for "Create new Git repository" if you would like the directory initialized as a local repository.

![](/images/vs-install_16.png)

I like to have the test files put in a test folder, so you can create a folder and just drag that test file into that folder. The next step is to right-click on the project and go to Properties so you can set the manifest information:

![](/images/vs-install_17.png)

I only set the root module, this will be what is run when you do `Import-Module MyFirstModule`. I then gave it a description and adjust the version information to my preferences. You can use the GUI to adjust the other information in the manifest or simply open the "psd1" file in the editor. It is just your preference, although I did find that updating the file directly does not seem to update the UI properties for some reason (not sure if this is a bug or not).

I'm not going to go over module design and such in this post, but after you get done updating the manifest you are ready to start developing your new module. I'm going to next touch on starting with a currently published project on GitHub, called dbatools.

### Starting From Current GitHub Project

The majority of any PowerShell module worth its weight and use nowadays is found on the PowerShell Gallery, with the code hosted on GitHub as the source control provider. If you want to get started contributing to public PowerShell modules, whether they are from Microsoft or the community, I will walk through doing this with the [dbatools repository](https://github.com/sqlcollaborative/dbatools). The same steps will apply to any repository on GitHub that you can use VS as your development IDE.

#### Cloning the Repository

You can clone or do the initial pull of a repository a few different ways. It depends on whether you want to use the GitHub.com interface or VS itself. It is best to use VS as this will also initialize Git for that local folder (repository).

To start you will go to the "Team Explorer" window and click on "Clone". You will need to provide the URL to the GitHub repository, in this case, I'm using my forked repository of dbatools. Just provide a local path, you can use the default if you want but I keep all of the repositories I contribute to under `C:\GitHub`

![](/images/vs-install_18.png)

Just click on the "Clone" button and it will begin to pull down all the files for the repository. Once that is complete VS will open the Solution Explorer and you will see the folder view of the dbatools modules.

![](/images/vs-install_19.png)

If you click on the "Solutions and Folders" button you will notice with the dbatools repository there is a solution file found. This is the C# project for the "dbatools.dll" and library source code. If you are interested, selecting the "sln" file will open that view in Solutions Explorer and you can traverse the code for that side of the module.

### Caveats with PowerShell Projects

With projects already on GitHub or hosted from another provider, unless the author uploaded the project as a Visual Studio PowerShell module project you will not be able to utilize features of the extension. Sadly there is no method or process in Visual Studio that lets "import" a non-project into a project template. Your only option would be to manually add the folders directly to the project file (via xml elements) and then you can add the files all at one time. It is a very manual process sadly.

Some time down the road maybe Adam or someone from the VS team will offer the ability to import folders and files into a project more easily, but right now it is an all manual process. If you are comfortable using Visual Studio you will find the time worth it, because it would just be a one time thing with the exception of new files from the repository being added upstream.