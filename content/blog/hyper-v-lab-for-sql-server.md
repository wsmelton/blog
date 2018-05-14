---
title: Hyper-V Lab for SQL Server
date: 2016-11-14T08:00:00-06:00
draft: false
---

Whether you are playing with features or learning them in a server operating system, or SQL Server, you need to first have somewhere to run it all. All of us would love to have a server rack in our garage/basement/workshop, but that incurs a pretty high cost. You might consider using Azure or AWS services, which for the most part are a good source. Once you get into working with SQL Server though, the price for both cloud providers can fluctuate pretty high based on what feature or component you want to play with or learn. If you have an offline lab that runs locally on your computer it makes it so much easier to go at your own pace, and not worry about what the bill will be each month.

# Virtual Software Options

You have a few options here, but the most popular you will see folks mention:

- <a href="https://www.virtualbox.org/" target="_blank">Oracle VM VirtualBox</a>
- <a href="https://www.vmware.com/products/player/playerpro-evaluation.html" target="_blank">VMWare Player</a>
- <a href="https://www.vmware.com/products/workstation.html" target="_blank">VMWare Workstation</a> (Requires $$$)
- <a href="htts://technet.microsoft.com/en-us/library/hh857623.aspx" target="_blank">Client Hyper-V</a> (Used to be called Virtual PC prior to Windows 8)

I have had the luxury of using each one of these through my career and they all work well. It just depends on what features you prefer and are more attracted to as to which one you should use. It will really depend on what part of the OS or SQL Server you want to try as to which one you can use. If for example you want to play with clustering or Availability Groups, VMWare Player is not something you can use because it does not support the virtual switch required for your servers to talk to each other. Just make sure you do your research before jumping into one over the other.

## My preference

I have favored Hyper-V since I moved to Windows 10 on my primary machine. It just seems to perform the best over the other products above I tried on my hardware. A <a href="https://www.pythian.com/blog/update-on-home-learning-lab-hyper-v/" target="_blank">co-worker blogged about his likes/dislikes with Hyper-V</a> when it came out for Windows 8. While most of his dislikes have not been necessarily fixed, you just have to understand: Hyper-V is a server technology that was adjusted to fit on a client OS. You are not going to have direct, or seamless, interaction with the servers as you will find the other products like VirtualBox or VMware Workstation. In Hyper-V world you interact with the servers just like you would in a production environment: using Remote Desktop or putty (depending on the OS flavor). If you follow this you will see most of the dislikes noted become obsolete.

One cool thing you get with Hyper-V is the ability to manage the virtual machines through PowerShell. It allows a much smoother and repeatable build process for the VMs. The OS install is still clicking (or typing) through the wizards. Though, for me Window Server 2012 R2 does not take all that long to install. You can save some time with the OS installations by building out a template to use. The template in this case is just the VHDX file you create as the system drive. You can sysprep the OS and then copy that file over and over, once you copy and attach it to a new VM you get a running Windows Server VM.

# Building the Lab

Obviously what you build is based on what you want to play with, or learn against. In most cases though, with any lab for SQL Server your lab will include a domain controller and then the server(s) running SQL Server. My preference on the domain controller is to utilize Windows Server 2012 Core Edition, for a handful of reasons:

1. No GUI = no resources used to render it all.
2. Smaller footprint - less storage required.
3. Tremendous cut down on Windows Updates that are required.

So while most everyone already knows how to install the full edition of Window Server, Core Edition can be a challenge. Instead of filling this post with screenshots I decided to build out a slide deck on building a full lab with Hyper-V. This slide deck walks you through the PowerShell commands for Hyper-V, and then setting up a server running Core Edition as a template. I also include walking through building a server using the template.

I have a <a href="http://blog.wsmelton.info/slides" target="_blank">slide deck landing page</a> that you can find the slide deck, or you can go to it directly from <a href="http://blog.wsmelton.info/slides/hyper-v-lab-build" target="_blank">here</a>. The slide deck requires no special software or plugins to view. It is broken down into the following sections that you can jump right to if you want:

- <a href="http://blog.wsmelton.info/slides/hyper-v-lab-build/#/2" target="_blank">Virtual Network Switch</a>
- <a href="http://blog.wsmelton.info/slides/hyper-v-lab-build/#/6" target="_blank">Create a VM</a>
- <a href="http://blog.wsmelton.info/slides/hyper-v-lab-build/#/10" target="_blank">Building a Template</a>
- <a href="http://blog.wsmelton.info/slides/hyper-v-lab-build/#/16" target="_blank">Create VM using the Template</a>

I did not include building a domain controller under Windows Core Edition...working on that for the next post.

# Summary

Hope you found the information and slide deck informative, and be sure to check back for the Active Directory deck.

<i><a href="https://flic.kr/p/6gYLHR" target="_blank">Header image source</a></i>

The content of this post can also be found <a href="https://www.pythian.com/blog/hyper-v-lab-for-sql-server" target="_blank">here</a>.