---
title: PowerShell Debugging
aliases: [/powershell-debugging]
date: 2017-10-30T12:30:00-06:00
draft: false
---

## The what and why

Debugging code can be a fun undertaking whether you just want to figure out why something broke or how it works. As well, in the age of "everything is a module" in PowerShell we can't discount having the ability to troubleshoot why a function or command does not do what is expected.

An alternative is to just fill your script(s) with `Write-Output` and `Write-Debug` statements. Which work, but is time consuming to put in on something you already wrote. As well, removing it and hoping you don't forgot a statement can be a bit embarrassing to deal with if you already released the changes.

Using either the PowerShell debugger itself or debugging features in your PowerShell editor of choice makes it much more efficient to both discover bugs and dig into how something may work.

_TL;DR_: This post will go over debugging as it pertains to PowerShell and the editor Visual Studio Code ("VS Code" or just "Code").

## Debugging in General

If you have never had to debug code whether it was PowerShell or even more formal programming language like C#, don't stop reading. It is not as complicated as you might think. I'm going to start in this post by going over some general concepts of debugging, as it pertains to PowerShell. The last bit I will go over some specifics on using Code to debug. I will have another post that will walk through actually debugging an issue in the [dbatools module](https://dbatools.io) I worked in previously. [_I actually learned some things in this instance._]

### Debugger

By definition:

> A program designed to help detect, locate, and correct errors in another program. It allows the developer to step through the execution of the process and its threads, monitoring memory, variables, and other elements of process and thread context. [Reference: Microsoft Debugging Terminology](https://msdn.microsoft.com/en-us/library/windows/desktop/ms679306(v=vs.85).aspx)

PowerShell has a debugger builtin that lets you dig into a specific script or function in a module. You actually can now see the source code for the debugger in PowerShell on [the GitHub repository](https://github.com/PowerShell/PowerShell/tree/ffd39b2853b68419eb0fd5e34a89b755c98b8022/src/System.Management.Automation/engine/debugger), if you are in to that type of thing.

### Breakpoints

Now it does not serve much purpose to debug your script if you execute it and it runs through the whole command. In debugging you want it to pause at certain statements so you can view or investigate what is going on up to that point. You do this by setting breakpoints.

In the PowerShell debugger there are three types of breakpoints:
1. Line
2. Variable
3. Command.

They are exactly what you would think as well. The most common used is the line breakpoint. The line breakpoint means it will stop at that statement on the line you set the breakpoint, it will not execute it. The variable and command allow you to set a breakpoint either when a variable changes value or before the specified command is about to execute.

## Tools

I am an avid user of [Code](https://code.visualstudio.com). It offers the ability to have a UI when you debug PowerShell code. If you have ever used [the ISE to debug PowerShell scripts](https://docs.microsoft.com/powershell/scripting/how-to-debug-scripts-in-windows-powershell-ise), then you may see some similar actions taking place in Code. The UI in Code offers a good bit more than ISE.

### VS Code and PowerShell

One thing to understand using Code is there is a difference between the temrinal that runs `PowerShell.exe` host, and the PowerShell Integrated Terminal that is part of the PowerShell extension. When you first open a PS1 file or set the format of a file to PowerShell, that integarted terminal is going to start up. This is a custom built host and one that is important to both the editor and debugger. This intergrated terminal is a completely custom host built via the [PowerShellEditorServices](https://github.com/PowerShell/PowerShellEditorServices/issues). With a custom host you simply need to understand it just does not work the same as the PowerShell host.

The authors of the PowerShell extension do their best to have the experience as close to the PowerShell host but there are some limitations. Majority of them are around Code itself just not offering the ability. They try to work around it when possible but in other areas it is just not possible (e.g. progress bars). The service and the extension, together, give you the total experience in Code for PowerShell development.

Just make sure to keep it in the back of your mind when your script is not executing or doing something you expect. Just give it a quick test in the PowerShell host and verify.

### Code Launch Configuration

Before you can start debugging any language in Code you have to configure it for that language. The first time you try to hit **F5 to start debugging** you will get a prompt to configure a launch configuration. (_I have seen some issues reporting in VS Code's repository that this may change in the future, but as of this post has not_). Once you select PowerShell it will throw in 4 options or methods you can use to debug PowerShell code. In this post, and my general practice, I only use the interactive configuration to debug modules as it works the best for me. I remove all other configurations to keep things simple. You can always play around with each one as you want to learn what they do. The interactive configuration will look like the below json:

```json
{
	"type": "PowerShell",
	"request": "launch",
	"name": "PowerShell Interactive Session",
	"cwd": "${workspaceRoot}"
}
```

This configuration will start the debugger, launch the integrated terminal and set focus to it. Once you are in the integrated terminal make sure you have breakpoints set for the function you want to debug, and then load the module into that debug session and execute the command/function you want to debug. If all works correctly you should stop at the first breakpoint you set in that function.

### Code Step'n

Once you hit a breakpoint, what do you do next? You have a number of choices:

![](/img/debug_step_options.png)

#### Start/Continue

Executes to the next breakpoint or completes execution of the script.

#### Step Over

Executes the current statement and stops at the very next one. In a module if that statement is a call to another function then that function will be executed as a whole, and then the debugger moves to the next statement.

#### Step Into

Executes the current statement but if the statement is another function (as in a module) or script, then the debugger will step into that function or script; otherwise it stops at the next statement. If you stepped into another function you can continue using step into to go through that function (or script). Once you are done in that function or script, you will be taken to the next statement in the original code.

#### Step Out

This one takes on various actions based on where you are at in the code.

1. If you are in a nested loop, it will step out of that onto the next statement.
2. If you are in the main part of the function or script (not in a loop), it will be the same as hitting Continue and will execute all statements to the end of the function or script.

#### Restart/Stop

Stop or restart the debugging session.


### Pretty Pictures is Everything

The documentation referenced for using ISE to debug goes into pretty good detail on how to use it but does not show much in the way of pretty pictures. In that documentation you can read up on the steps to take for debugging in the ISE so I'm not going to repeat that part, but I will provide a bit of comparison on the visual side. The visual appeal of using editors is what tends to drive folks to using one more than the other. As well, you can be more efficient with some editors than you are with others, at least for me.

One of the main differences between using ISE or Code is the UI itself. You can do the basic line breakpoints in the ISE, but a good portion of interacting in the debug environment itself is via the debug commands built into PowerShell. [_Which the [debugging commands have been here since PowerShell version 2.0](https://technet.microsoft.com/en-us/library/ff730925.aspx#E2) and when you are in a pinch can be useful._] I also point out that you can use the debug commands for Code as well, the debug engine will honor breakpoints set using those commands.

#### Line Breakpoints

Line breakpoints are going to be the most commonly used type you will generally use. **F9 is used to toggle breakpoints** on and off for both editors. Visually, though, there is a bit of a difference in how each editor shows the reference that a breakpoint is set:

![](/img/debug_Code_vs_ISE.png)

Now when you get to a point where you have multiple breakpoints this is where the ISE gets left behind. In the ISE you have a menu option to list all breakpoints, but all that does is run `Get-PSBreakpoint` command and output it to the console. Code, will give you a nice view in the debug panel of the breakpoints you have:

![](/img/debug_Code_list_breakpoints.png)

#### Other Breakpoints

In the ISE `Set-PSBreakpoint` is used to set other types of breakpoints. In Code they are done in various ways from the UI perspective. The [documentation goes over the additional options](https://code.visualstudio.com/docs/editor/debugging#_breakpoints) pretty well and I'm not going to repeat that in this post.

## Summary

Debugging can be a frustrating experience and a learning experience at the same time. You may know how something "should" work but when you debug it shows you what it is doing. I have had a few eye openers when debugging code, it is pure fun. In my next post I will walk you through one of those experiences where I learned something by debugging. The next post will have some more pretty pictures as well.

Header image provided via [pixabay](https://pixabay.com/en/fly-swatter-flyswatter-fly-flap-bug-149265/)