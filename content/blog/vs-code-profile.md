---
title: "VS Code Profile"
date: 2018-06-07T08:00:00-05:00
draft: false
tags: [vscode]
---

If you have not started using Visual Studio Code just yet you can take a look at the [intro videos on the basics](https://code.visualstudio.com/docs/introvideos/basics). One item that is dug into the documentation that I have commonly seen asked on SO a few times is around the PowerShell extension and the extension's Integrated Terminal.

The main question asked is around creating the profile, or they already have a profile for PowerShell but the integrated terminal is not "seeing" it (or picking it up). There is one primary reason for this: Integrated Terminal has a dedicated profile script that is different than PowerShell's.

### PowerShell Host

It helps to understand one point of confusion sometimes around VS Code and using it as a development tool for PowerShell. Don Jones did a great write up on [the shell vs the host](https://powershell.org/2013/10/19/the-shell-vs-the-host/) where he explains that `PowerShell.exe` is the host application that interacts with the engine that is PowerShell under the covers. So when you hear folks refer to "the shell", "console" and such they are referring to the host application that is `PowerShell.exe` most commonly.

In VS Code and the PowerShell extension you have the option of two host. You can use the terminal in VS Code that is by default set to `PowerShell.exe`, this exist whether the extension is present and enabled or not. When you are interacting with the PowerShell extension using the editor or executing some code with F5 or F8 keyboard shortcuts on Windows, it utilizes an a custom host. The integrated terminal offered with the PowerShell extension is a custom built extension based on the [PowerShellEditorServices module](https://github.com/PowerShell/PowerShellEditorServices) (PSES).

In that regard it is just something to keep in mind that scripts you run in VS Code can act a bit different between running them in the PowerShell terminal versus using the PowerShell Integrated Terminal. The main thing I see most often is with just format of the output, but this is being fixed and improved with each release.

### Profiles

You can find the path of the profile script for the given host by simply executing `$PROFILE` in it. That will cause the path of the file to be displayed for you. If you have never created the file before you can run this command to create it:

```powershell
New-Item $PROFILE -ItemType File -Force
```

In `PowerShell.exe` when you inspect the variable `$PROFILE` you will see that it points to `$env:USERPROFILE\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1`. This is the file that gets loaded when you start `PowerShell.exe`. All of the profiles for Windows PowerShell will be created in this same directory. In PowerShell Core it will be under `.\Documents\PowerShell`.

You also have a separate profile with PowerShell ISE and with VS Code. In VS Code the file name is `Microsoft.VSCode_profile.ps1`.

Now I for one was not up to keeping two different profiles and much prefer to just keep one. So you can actually use a trick to dot source your main profile (`PowerShell_profile.ps`) in your VS Code profile (`VSCode_profile.ps1`). This will allow updates to your main profile to get picked up in VS Code.

### Dot sourcing Profile

Just create your profile for VS Code and paste the below contents into the file:

```powershell
. $PSScriptRoot\Microsoft.PowerShell_profile.ps1
```

Two things to point out:

1. The dot at the start of the line is the method used to dot source your script. This will cause the contents of the profile ps1 to load into your VS Code profile.
1. The `$PSScriptRoot` is a built-in variable for PowerShell that basically points to the current directory of the host. So in this case VS Code's terminal or the PowerShell Integrated Terminal both point at the directory for your `$PROFILE` path.

### Exiting

I hope this was helpful in explaining a few things around VS Code and using it for PowerShell development. It is a wonderful tool but does take a bit to get used to using it. Give it time and it does grow on you.