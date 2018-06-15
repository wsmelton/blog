---
title: Building AD Domain on Windows Core Edition
date: 2016-12-03T11:42:00-06:00
draft: false
---

This is a follow up post <a href="2016-11-14-hyper-v-lab-for-sql-server.md" target="_blank">on building an Hyper-V lab</a> to learn SQL Server.

Active Directory offers the PowerShell module <a href="https://technet.microsoft.com/en-us/library/ee617195.aspx" target="_blank">ActiveDirectory</a> for managing various aspects of the domain. If you are a full-time AD Administrator you may need to learn the commands in this module in great detail, but for lab purposes we only need to be familiar with a few of them. However, first things first...we need to create our domain in the lab.

# Building the Domain

If you recall from the previous post we built out a server running Windows 2012 R2 Core Edition. You can <a href="https://blog.wsmelton.info/slides/hyper-v-lab-build/#/10" target="_blank">check here</a> to see how that server was configured.

There were some initial tools that we installed on that server but to actually create the domain you have to install 2 specific Windows features. You can do that with the following command:

```powershell
    Install-WindowsFeature AD-Domain-Services,RSAT-ADDS
```

The feature "RSAT-ADDS" installs the needed module ADDSDeployment that includes the command we need to create our first Active Directory Forest. Just to provide a little bit of context, in a lab setting our first domain is the top-level forest, but in real-world you can have a top-level forest domain that has multiple sub-domains.

The "AD-Domain-Services" feature is the services and binaries requires to run the Active Directory Forest itself.

## Secure String

One thing to remember with some modules in PowerShell is when you need to pass in a password, most of the commands do not allow you to simply pass in a string value. They will require a specific string type for that password: <a href="https://msdn.microsoft.com/en-us/library/system.security.securestring(v=vs.110).aspx" target="_blank">System.Security.SecureString</a>.

There are a few ways to create this type of object:

```powershell
    # Passing in the password on the command line prompt (in plain text)
    $pwd = ConvertTo-SecureString -String 'MyT0p#3cr3tP@ssw0rd' -AsPlainText  -Force

    # More secretive method that does not show the password to anyone watching over your shoulder
    $pwd = (Get-Credential).Password
```

The second part I generally use and is most common, but I will show both in this article.

## Create that Forest

The command to create your forest is "Install-ADDSForest", and it has a lot of parameters to build the forest. In order to make it readable I formated the table below, but just understand that this is a one-liner to execute on the server. First though we need a few lines of code to get the one password we need to pass to the command:

```powershell
    $SafeModeAdminPassword = ConvertTo-SecureString "Your choice of password" -AsPlainText -Force
```

<table>
    <tr>
        <th>Parameter</th>
        <th>Value</th>
        <th>Example</th>
    </tr>
    <tr>
        <td>CreateDNSDelegation</td>
        <td>$false</td>
        <td>-CreateDNSDelegation:$false</td>
    </tr>
    <tr>
        <td>DatabasePath</td>
        <td>C:\Windows\NTDS</td>
        <td>-DatabasePath "C:\Windows\NTDS"</td>
    </tr>
    <tr>
        <td>DomainMode</td>
        <td>Win2012</td>
        <td>-DomainMode "Win2012"</td>
    </tr>
    <tr>
        <td>ForestMode</td>
        <td>Win2012</td>
        <td>-ForestMode "Win2012"</td>
    </tr>
    <tr>
        <td>DomainName</td>
        <td>LAB.LOCAL</td>
        <td>-DomainName "LAB.LOCAL"</td>
    </tr>
    <tr>
        <td>DomainNetbiosName</td>
        <td>LAB</td>
        <td>-DomainNetbiosName "LAB"</td>
    </tr>
    <tr>
        <td>InstallDNS</td>
        <td>$true</td>
        <td>-InstallDNS:$true</td>
    </tr>
    <tr>
        <td>LogPath</td>
        <td>C:\Windows\NTDS</td>
        <td>-LogPath "C:\Windows\NTDS"</td>
    </tr>
    <tr>
        <td>NoRebootOnCompletion</td>
        <td>$false</td>
        <td>-NoRebootOnCompletion:$false</td>
    </tr>
    <tr>
        <td>SysvolPath</td>
        <td>"C:\Windows\SYSVOL"</td>
        <td>-SysvolPath "C:\Windows\SYSVOL"</td>
    </tr>
    <tr>
        <td>Force</td>
        <td>$true</td>
        <td>-Force:$true</td>
    </tr>
    <tr>
        <td>SafeModeAdministratorPassword</td>
        <td>$SafeModeAdminPassword</td>
        <td>-SafeModeAdministratorPassword $SafeModeAdminPassword</td>
    </tr>
</table>

Once you run this command you will see some action occurring while the forest is being built. Your server should restart once the command completes. You will login as the Domain Administrator using the same password you set for the local Administrator account, once the server restarts.

# Active Directory Commands

The module you will use to work with Active Directory is named appropriately "ActiveDirectory". There are only are a handful of commands we need to remember to manage our lab environment. You can obviously utilize "Get-Help" to see more details on the commands, but just for reference I'll give examples of the ones I use most often.

## Get-ADUser

```powershell
    Get-ADUser -Filter * -Properties Description | select Name, SamAccountName, Enabled, Description | ft -auto
```

![](/img/lab_ad_domain_getaduser.png)

The "Filter" parameter is required for this command, and then the "Properties" is used to pull back properties that are not output by default (e.g. Description, PasswordExpired, etc.). You can use an asterick to have every property, but would stress doing this only in your lab environment.

## Get-ADGroup

```powershell
    Get-ADGroup -Filter * | select Name, SamAccountName | ft -auto
```

![](/img/lab_ad_domain_getadgroup.png)

## Get-ADGroupMember

![](/img/lab_ad_domain_getadgroupmember.png)

```powershell
    Get-ADGroup -Filter * | select Name, SamAccountName, GroupCategory, GroupScope | ft -auto
```

This command returns an "ADPrincipal" object, which is similar to the "ADUser" object that is returned by "Get-ADUser", the exception is you only get a subset of properties on that user/group.

## New-ADUser

One prerequisite that is needed to create an account is providing the password. Which for my lab environment I just use the same password for any account I am creating.

```powershell
    $pwd = ConvertTo-SecureString "P@ssword123" -AsPlainText -Force
    New-ADUser -Name 'Bob The Builder' -SamAccountName BobTheBuilder -PasswordNeverExpires $true -AccountPassword $pwd -Enabled $true
```

![](/img/lab_ad_domain_newaduser.png)

## New-ADGroup

One parameter to note ont his command is the <a href="https://technet.microsoft.com/en-us/library/cc755692(v=ws.10).aspx" target="_blank">Group Scope</a> parameter. This parameter has 3 options: Global, DomainLocal, Universal. Setting this to Global is sufficient for your lab environment.

```powershell
    New-ADGroup -Name Tractors -GroupScope Global
```

![](/img/lab_ad_domain_newadgroup.png)

## Add-ADGroupMember

The 2 parameters you deal with are the identity (group you want to work with) and members (AD identities to add to the group). You can add a single member using this command or multiple, as the members parameter will accept an array of values.

```powershell
    Add-ADGroupMember -Identity Tractors -Members Scoop,Stretch
```

![](/img/lab_ad_domain_addadgroupmembers.png)

## Set-ADAccountPassword

You will need this to change the password for a given account. In this example I just show how you can use the "Get-Credential" command to pass in the password.

```powershell
    Set-ADAccountPassword -Identity BobTheBuilder -Reset -NewPassword (Get-Credential).Password
```

![](/img/lab_ad_domain_setadaccountpassword.png)

## Unlock-ADAccount

For those situations where you locked an account, there is nothing special about this command.

```powershell
    Set-ADAccountPassword BobTheBuilder
```

## Set-ADUser

I'm not going to show any examples on this one, but just bring it up. If you happen to be doing any testing with AD scripts and you want to set some of the many properties for a given account, then you can use this account. You can find all the various parameters that can be used <a href="https://technet.microsoft.com/en-us/library/ee617215.aspx" target="_blank">here</a>.

The content of this post can also be found <a href="https://www.pythian.com/blog/building-ad-domain-on-windows-core-edition" target="_blank">here</a>.