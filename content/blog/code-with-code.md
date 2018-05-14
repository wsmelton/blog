---
title: Code with Code (for Windows)
aliases: [/vs-code]
date: 2016-12-24T06:30:00-06:00
draft: false
tags: [vscode]
---

In a<a href="/2016-10-19-powershell-editors" target="_blank"> previous post on PowerShell Editors</a> I included Visual Studio Code (Code) in that list. In this post I wanted to introduce Code a bit more to you, and walk you through how you can interact with GitHub repositories. I mean now a days, who doesn't have a GitHub account?

_Now I will make a caveat that I'm not going to go into the workflow and details of how Git works. There are books written just for this topic if you want to master it. If you want to learn from the ground up I would suggest checking PluralSight for courses by Paolo Perrotta. He has two courses published at the time of this post on "How Git Works" and "Mastering Git"._

GitHub is used anywhere from just a script library to hosting open source projects like <a href="https://msdn.microsoft.com/powershell" target="_blank">PowerShell</a>. I was not full time user of Code initially, going between Visual Studio and then Code for various things. However, after I forced myself to use it more frequently it became more of my go to editor, especially after figuring out the GitHub stuff a bit more. I started to contribute to a SQL Server Community project called <a href="https://dbatools.io" target="_blank">dbatools</a> on GitHub, and Code is my primary editor for that project now.

Contributing to dbatools varies from having an opinion, reviewing code, testing, and even writing some PowerShell. It offers a nice challenge to see new styles and some cool things done in PowerShell. You can also learn just by reviewing, and reading through the lines of code (over 35,000). In this post I will use dbatools repository as an example with Code and GitHub integration.

# Starting point

You will first need to <a href="https://code.visualstudio.com/download" target="_blank">download</a> and install Code. If you are one that likes to be on the cutting edge, you can <a href="http://code.visualstudio.com/insiders" target="_blank">download and run the Insider's build</a>. The identifier to know which one you are running is the stable version has a blue icon, and the insider's build is green.

There are a few sections of the documentation I would highly recommend you read through. The sections noted below will give you a good idea of how to maneuver around the editor.

- <a href="https://code.visualstudio.com/docs/customization/userandworkspace" target="_blank">User and Workspace Settings</a>
- <a href="https://code.visualstudio.com/docs/customization/keybindings" target="_blank">Keyboard shortcuts</a>
- <a href="https://code.visualstudio.com/docs/editor/integrated-terminal" target="_blank">Integrated Terminal</a>

These two articles offer some very good tips and tricks that helped me while I was getting started as well:

- <a href="https://github.com/Microsoft/vscode-tips-and-tricks" target="_blank">Microsoft's collection of helpful tips and tricks</a>
- <a href="http://donovanbrown.com/post/visual-studio-code-keyboard-shortcut-cheat-sheet" target="_blank">Donavan Brown's keyboard shortcut cheat sheet</a>

# Git

While Code does integrate with Git, it does not come with it by default. You will need to <a href="https://git-scm.com/download/win" target="_blank">download Git</a> to your machine. The installation is simple and you can just accept the defaults.

Once you do that now we can get started with interacting with a public GitHub repository.

# Fork It and Clone

You browse to the <a href="https://github.com/sqlcollaborative/dbatools" target="_blank">dbatools</a> repository on GitHub, and can fork it to your account. Once you do that we simply need to grab the URL to clone it in Code.

Click on the "Clone or download" button, and then click the copy button for the HTTPS URL.

<img src="/img/codewithcode_clonedbatools1.png" />

Now open Code, and using the Command Pallete (CTRL+SHIFT+P) we can clone the repository. Type in "git" and you see all the commands available.

![](/img/codewithcode_clonedbatools2.png)

We want to use "Git: Clone", which you can type that specifically or hit your space bar and start typing "clone". Once you get the phrase unique enough to only show the command you want in Code you can just hit enter.

![](/img/codewithcode_clonedbatools3.png)

Enter the URL for your fork of the repository:

![](/img/codewithcode_clonedbatools4.png)

Select the folder you want the repository to be cloned to:

![](/img/codewithcode_clonedbatools5.png)

You will see an information prompt showing that it is cloning (or downloading) the repository:

![](/img/codewithcode_clonedbatools6.png)

Now after all that is done you should get a view similar to this in Explorer of Code:

![](/img/codewithcode_clonedbatools7.png)

# Branch

Branches are a way to separate out what you are working on. Each branch you create is a copy of the current branch you have checked out. In dbatools we want to start out with the development branch, this has most of the "new" changes that are going to be wrapped in the next release. Creating a branch is pretty simple, just use the "Git: Branch" and enter a name of the branch. I created one called "BlogPost" to work through in this post.

Once you create the branch you will just need to issue the "Git: Publish" command. You can then start making commits to the branch.

# Commits

As an example I'm just going to make a change to a command, and then commit it to the BlogPost branch. One thing the PowerShell extension provides in code is the ability to check the code against the <a href="https://github.com/PowerShell/PSScriptAnalyzer" target="_blank">PSScriptAnalyzer</a>. This ensures best coding practices are followed, and dbatools adhers to the rules in this tool for the code that is submitted. If I go to "Get-DbaDiskSpace.ps1" I can see one such rule in PSScriptAnalyzer is violated:

![](/img/codewithcode_commit1.png)

All we need to do to resolve this is remove the "object" and make it a PSCredential type. You can see the intellisense in the PowerShell extension helps us get this changed out quickly.

![](/img/codewithcode_commit2.png)

Now when you save the file you will see the green squiggle line disappear, and in the view bar you can see the Git icon shows we have an uncommitted change. Keyboard keystroke to bring up the Git side bar is CTRL+SHIFT+G.

![](/img/codewithcode_commit3.png)

You can use the side bar to enter a commit message. I happen to know at the time of this posting there is an issue open on dbatools for the change we made: <a href="https://github.com/sqlcollaborative/dbatools/issues/379" target="_blank">Issue 379</a>. In this example I did not address all of the items in that issue, but we will pretend we did. The commit message you use is very important in most cases for repositories. When you do a commit you want to include <a href="https://help.github.com/articles/closing-issues-via-commit-messages/" target="_blank">a keyword and the issue number</a>. This will allow GitHub to perform its magic when your pull request gets merged, as it will auto-magically close that issue.

The first line of your commit message is the title. You can hit enter and continue adding more details as a comment.

![](/img/codewithcode_commit4.png)

Now one warning message you will see on your first commit is setting your user name and email:

![](/img/codewithcode_commit5.png)

This is easily remedied by opening up the integrated shell and using the following commands to set it. This information is added to every commit you do to a GitHub repository:

```git
git config --global user.name "Your Name"
git config --global user.email "Your Email"
```

After that just commit again and then sync to upload that commit to your repository. After this you just need to do a <a href="https://help.github.com/articles/about-pull-requests/" target="_blank">pull request</a> to dbatools development branch. If approved your contribution will be merged into development. Once a release is built development changes are merged into master to be made public.

# Miscellaneous Items

There are a few things that you will find a need to perform during your time contributing to public repositories, like dbatools. This is not exhaustive but goes over a few of the main items I found myself having to do frequently.

The group with dbatools favor putting changes (whether bug fix or new feature) into a new branch. It does help once you get active and working on multiple commands to keep your work separated. However, in doing that you need to ensure the branch you are working with is kept current to the "upstream" development branch.

## Setup an Upstream

By default there is no upstream configured for your local repository. So we need to create an upstream that points to the dbatools repository. You will need to get the HTTPS URL for that repository by going to the <a href="https://github.com/sqlcollaborative/dbatools" target="_blank">home page of the repository</a>. Then you just execute this command in your Shell window:

```powershell
# see your current remote repositories
git remote -v

# add a remote called "upstream"
git remote add upstream https://github.com/sqlcollaborative/dbatools.git
```

## Keeping up-to-date

With your upstream setup we need to periodically check if we are behind or ahead of that upstream branch, development. This branch is particularly important because everyone's changes for the next release are merged into this branch. I tend do to this before I ever start any new contribution or if I've taken a break from working on something for a few days and will start back.

```powershell
# refresh the refs to the remote repository
git remote update

# see what has changed for a specific branch
git show-branch *development

# syncs all the changes made to upstream development branch
git pull upstream development
```

# Summary

Code is a great, lightweight editor for developing PowerShell or other languages. If you are a first timer in using Code I would encourage you to read through the documentation referenced above as it helped me to start liking the editor more and more. The only way to start using it more is to get involved in coding; contributing to dbatools is a great start down that road. If you are stuck or want to know how to get started just come find us on the <a href="https://dbatools.io/slack/" target="_blank">SQL Community Slack channel #dbatools</a>.

Git is a big topic and I am by no means an expert yet, but I hope you found some starting points with what I have shared. There are numerous locations online to get additional help and learn more about the terminology. I would encourage you to signup for the 30 day trial of PluralSight and go through the courses referenced.

The content of this post can also be found <a href="https://www.pythian.com/blog/git-and-visual-studio-code" target="_blank">here</a>.
