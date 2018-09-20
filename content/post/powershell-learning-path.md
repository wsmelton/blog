---
title: PowerShell Learning Path
aliases: [/powershell-learning-path/]
date: 2017-06-05T09:00:00-06:00
draft: false
---

How much do you automate in your job? The question is not necessarily specific to SQL Server, whether you work as a system administrator or even business analyst. There are areas of your job that can be, and should be, automated. Ok, now back to SQL Server specifics...

# Day-To-Day Task

A database administrator always has some mundane task to do each day, if they want to keep their job. These little things are the best candidates for automating, as a starting point. Once you get those automated you will see the benefit and it will help your mindset change to start thinking in that manner more and more.

# The Tool of Choice

One tool that is growing more and more each year in both features and use, is PowerShell. As a beginner you will ask, "what is PowerShell". I give you [this quote from The Scripting Guy](https://blogs.technet.microsoft.com/heyscriptingguy/2015/01/02/what-is-powershell/) at Microsoft that I think sums it up well:

> Windows PowerShell is an interactive object-oriented command environment with scripting language features that utilizes small programs called cmdlets to simplify configuration, administration, and management of heterogeneous environments in both standalone and networked typologies by utilizing standards-based remoting protocols.

# Learning Path

An endeavor at Pythian (my current employer) began a few months back to get folks mindset moved more toward automation. One of those paths for the teams that support Microsoft Data Platform products is PowerShell. I drew up a list of courses and books to give the team a learning path to take. Now mind you this is not an exhaustive list, just the ones I know worked for me and are well structured.

These are listed in order of progression, so if you are already familiar with certain areas you can skip over to the next.

## Microsoft Virtual Academy

### Getting Started with Microsoft PowerShell

- Total Time: 6 hours (excluding labs and such)
- Link: [here](https://mva.microsoft.com/en-US/training-courses/getting-started-with-microsoft-powershell-8276?l=r54IrOWy_2304984382)
- Summary: Jeffrey Snover goes over a good bit of background and just Microsoft’s intention with PowerShell. It has some very good information on how to get started. Anyone starting to learn it should watch this at most.

### PowerShell for SQL Data Professionals

- Total Time: 3 hours (excluding labs and such)
- Link: [here](https://mva.microsoft.com/en-US/training-courses/powershell-for-sql-data-professionals-16532?l=XgA5w0PgC_8805121157)
- Summary: Mike Fal is good guy I know from PowerShell world. He is DBA and has long background in SQL Server and using PowerShell with it. This course has good overview of the basics, and then dives in to automation for PS and SQL Server and some Azure stuff.

### Getting Started with PowerShell Desired State Configuration (DSC)

- Total Time: 6 hours (excluding labs and such)
- Link: [here](https://mva.microsoft.com/en-US/training-courses/getting-started-with-powershell-desired-state-configuration-dsc-8672?l=ZwHuclG1_2504984382)

- Summary: This is the platform for automating building of servers, and validating configuration of servers, with PowerShell. This includes speaking from Jeffrey Snover (creator of PowerShell) so will get more information on PS itself and DSC if they listen to it.

## Books

### Learn Windows PowerShell in a Month of Lunches, Third Edition

- Link: [Manning Publications](https://www.manning.com/books/learn-windows-powershell-in-a-month-of-lunches-third-edition)
- Description: This book walks you through PowerShell and provides just about everything you need to get down the basics of PowerShell. Most anyone that goes through this book comes out reading to automate.

### Learn PowerShell Toolmaking in a Month of Lunches

- Link: [Manning Publications](https://www.manning.com/books/learn-powershell-toolmaking-in-a-month-of-lunches)
- Description: Is next in the series for PowerShell lunches. Begins to go through how you write scripts as tools and not just a PS1 file that you run. Also starts into the advanced things of PowerShell such as error handling and debugging.

### The Pester Book

- Link: [Leanpub.com](https://leanpub.com/the-pester-book)
- Description: This book is in progress so you buy what is currently available and then will get free updates as the book is completed. It provides an excellent walk-through of what Pester is and how to start using it. Authors are Don Jones and Adam Bertram, same ones from Pluralsight courses.

### The DSC Book

- Link: [Penflip.com](https://www.penflip.com/powershellorg/the-dsc-book)

- Description: Book written for PowerShell 4.0 version of DSC, no longer being maintained but still relevant for learning DSC.

## Pluralsight

### Introduction to PowerShell

- Total Time: 2h 41m
- Link: [here](https://app.pluralsight.com/library/courses/powershell-intro/)
- Description: PowerShell is Microsoft’s full featured scripting language. Built on the .Net Framework, it is extensible, powerful, and easy to work with. In this course you’ll begin your path to PowerShell mastery by learning the basics, including: how to customize the User Interfaces; basic PowerShell commands; variables; loops; branching; script blocks; working with files; processing user input; creating and extending functions.

### PowerShell Toolmaking Fundamentals

- Total Time: 3h 55m
- Link: [here](https://app.pluralsight.com/library/courses/powershell-toolmaking-fundamentals/)
- Description: PowerShell can be many things to many different people. PowerShell can be a simple command-line replacement or a scripting language. Beginners to intermediate-level scripters are probably still writing one-liners and simple scripts. They’re probably starting to see the potential of PowerShell not as a simple scripting language but as a way to build “tools” to use over and over again. Don’t recreate the wheel. Learn how to create reusable scripts so you don’t have to recreate that wheel.

### PowerShell and SQL Server

- Total Time: 2h 48m
- Link: [here](https://app.pluralsight.com/library/courses/powershell-and-sql-server/)
- Description: This course is designed to teach you the fundamentals of using PowerShell to manage your SQL Servers, as well as develop on them. In Module 1, we cover basic DBA tasks using just PowerShell. With Module 2, we provide an introduction to the two main tools for working with SQL Server, the SMO, or SQL Management Objects, and the SQL Server Provider. Module 3 will cover basic DBA tasks using both SMO and the SQL Provider. With Module 4 we switch to Developer mode and cover development using the SQL Provider. Module 5 continues the developer theme, this time using the SQL Management Objects. We finally wrap things up with Module 6, in which we go over a real world example of using PowerShell and SQL Server. We also cover the SQL PS mode of PowerShell, as well as how to make effective use of PowerShell from a SQL Server job.

### Windows PowerShell Best Practices and Patterns

- Total Time: 2h 55m
- Link: [here](https://app.pluralsight.com/library/courses/windows-powershell-best-practices-patterns/)
- Description: Windows PowerShell MVP Don Jones helps you take your Windows PowerShell skills to a new, more professional level through the application of best practices and patterns. Developed and vetted by the overall PowerShell community, these patterns focus on maintainability, reliability, and conformance with native PowerShell approaches. Designed for administrators who are developing mission-critical and production-use PowerShell scripts, these patterns will help you - and your scripts - be taken more seriously.

### Formatting with PowerShell

- Total Time: 2h 28m
- Link: [here](https://app.pluralsight.com/library/courses/formatwithpowershell/)
- Description: This course takes a close look at a variety of mechanisms you can leverage to get great looking output from Powershell. The first two modules focus on string formatting and using the ToString() method. The rest of the course looks at using Format-\* cmdlets, hash tables, and using format files and Format XML.

### PowerShell Gotchas

- Total Time: 1h 40m
- Link: [here](https://app.pluralsight.com/library/courses/powershell-gotchas/)
- Description: PowerShell is the de facto standard for automation and administration on Windows systems. The central design mantra in PowerShell is Think-Type-Get. That is: Think what you want, Type it, and Get the results. Unfortunately this mantra doesn’t always work - PowerShell combines concepts from other languages (Perl, Python, and VBScript for example) and borrows ideas from other platforms (like pipelining in Bash). This creates an experience that feels familiar, but fails to behave consistently with our experiences. This creates “gotchas.” In this course, we will analyze some specific cases of PowerShell’s strange behavior in order to better understand how and why PowerShell works the way it does.

### Creating PowerShell Modules

- Total Time: 2h 33m
- Link: [here](https://app.pluralsight.com/library/courses/psmodules/)
- Description: PowerShell modules allow scripts, cmdlets and other assets to be integrated into PowerShell in order to extend its functionality. This course starts with an overview of PowerShell module fundamentals, and then proceeds to explore and explain script modules, binary and manifest modules, as well as dynamic modules. The course concludes with a look at how integrated help documentation for PowerShell scripts and modules can be created, deployed and updated.

### Building Advanced PowerShell Functions and Modules

- Total Time: 4h 0m
- Link: [here](https://app.pluralsight.com/library/courses/powershell-modules-advanced-functions-building)
- Description: In this course, we are going to cover nearly everything there is to know about advanced functions and modules. Overall, this course can be broken down into six main components: differences between basic and advanced functions, advanced functions and how to build them, leveraging the PowerShell pipeline in your advanced functions, how to build safeguards into your functions with WhatIf and Confirm support, building and managing script and manifest modules, and, finally, writing help content for both your advanced functions and modules.

### Windows PowerShell Desired State Configuration Fundaments

- Total Time: 2h 57m
- Link: [here](https://app.pluralsight.com/library/courses/powershell-desired-state-configuration-fundamentals/)
- Description: *This course lays out how DSC works very well.* This course is designed to provide an introduction to Desired State Configuration (DSC). With DSC, you create server configurations and deploy them to your servers. The best part is that you can leverage your PowerShell skills to easily create and deploy configurations. Desired State Configuration Fundamentals is designed to get you started as quickly as possible. It is assumed that the viewer has some previous experience in Windows PowerShell, including writing scripts in the PowerShell ISE, and is familiar with installing and configuring Windows servers and operating systems.

### Advanced Windows PowerShell Desired State Configuration

- Total Time: 3h 9m
- Link: [here](https://app.pluralsight.com/library/courses/advanced-powershell-dsc/)
- Description: The purpose of this course is to provide advanced coverage of PowerShell Desired State Configuration. The material in this course is what IT Pros who want to use DSC in their environments will be using in production. We’ll look at how to build and use a pull server, including deploying resources. We’ll also explore how to use certificates to create a secure DSC environment. The course will wrap up with walkthroughs of using DSC to configure Windows and Linux servers. This course will focus on DSC as it exists in PowerShell 4.0.

### Practice Desired State Configuration

- Total Time: 3h 1m
- Link: [here](https://app.pluralsight.com/library/courses/practical-desired-state-configuration/)
- Description: *Do not start this course unless you have completed the one above by Jeff Hicks.* The way you are expected to manage and administer Windows servers is changing. In this course, Practical Desired State Configuration (DSC), you’ll learn how to use Desired State Configuration by applying it to several real-world scenarios. First, you’ll learn how to expand DSC beyond its built-in resources by learning about custom DSC resources. Next, you’ll learn how to secure DSC. Then, you’ll learn how to build and administer Active Directory with DSC. Lastly, you’ll learn how to set up and configure Windows Event forwarding with DSC. When you’ve finished this course, you’ll have the skills and knowledge required to securely bring DSC into your environments.

### Testing PowerShell with Pester

- Total Time: 4h 11m
- Link: [here](https://app.pluralsight.com/library/courses/powershell-testing-pester/)
- Description: *A very good storyline naritive to show how Pester is used.* Having a good testing framework will ensure your PowerShell scripts function as designed, and will ensure they continue to work correctly after you make changes. In this course, Testing PowerShell with Pester, you’ll learn how to use Pester, the new open source testing tool, to create tests for all of your PowerShell scripts and modules. You’ll start with seeing how to use Pester to test an existing code base. After that, Pester will be used to validate change requests to a module. Finally, you’ll use Pester along with Test Driven Development to craft a brand new module. After watching this course, you’ll have the confidence to test and use your own PowerShell scripts in your own projects.