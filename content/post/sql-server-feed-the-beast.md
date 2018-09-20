---
title: SQL Server - Feed the Beast
date: 2015-10-22T08:00:00-06:00
drafts: false
tags: [powershell,sqlserver]
---

_This content was originally posted on [here](https://www.pythian.com/blog/sql-server-fast-food/)._

An environment where you have a high number of databases on one server, or many, can be time consuming to something as simple as adding a user account. You have the option of using the GUI with SQL Server Management Studio (SSMS), which if it was a rush to get something in place for 8 or 10 databases I can see possibly doing that to get it done. You could do this with a bit of typing using T-SQL and a cursor or that famed, undocumented procedure `sp_MSForeachdb`.

I recently had a request from a customer that fell into the above scenario and used PowerShell to handle the request. I just wanted to show how I went about getting it done. I think this is a situation where both T-SQL or PowerShell will work, I just picked the one I wanted to use. Breaking this down, these are the basic steps I had to perform:

- Check for the login
- Create user
- Create role
- Assign INSERT and UPDATE to the role
- Add the user to the database role

All in all, that is not too much, if you understand how PowerShell and SMO work for you. If you are not familiar with PowerShell you can reference the recent series I published on the <a href="http://www.pythian.com/blog/pillars-of-powershell-interacting/" target="_blank">Pillars of PowerShell</a> that should help you get started. When I was learning PowerShell I always found I learned the best by reading through other folks scripts to find out how stuff was done. You can find the full script at the end of this post if you want to just skip right to it, I won't be offended.

One thing I always find useful with SMO is remembering that MSDN documents everything for the namespace <a href="https://msdn.microsoft.com/en-us/library/microsoft.sqlserver.management.smo%28v=sql.120%29.aspx" target="_blank">Microsoft.SqlServer.Management.Smo</a>. If you spend the time to review it and at least get familiar with how the documentation is laid out, using and finding answers for things with SMO becomes much easier.

### The Bun

As always the first step is going to be to create the object for the instance or server:

```powershell
$s = New-Object Microsoft.SqlServer.Management.Smo.Server $server
```

The task of verifying the login exists, I utilized one of the common methods that is available with a string type, `Contains()`. Now you generally use the `Get-Member` cmdlet to find the various methods available for an object, but this particular one does not show if you were to run: `$s.Logins | Get-Member`. There are a set of methods that follow each type of value (e.g. String, integer, date, etc.) and the `Contains()` method is one with the string type. There are two ways I have found to discover these type of methods:

- Pass the value type to `Get-Member` [e.g. `"A string" | Get-Member`]
- Use tab completion [e.g. Type out "$s.Logins." with the period on the end, and then just start hitting the tab key]

_If you want a bit of exercise you can see if you can add in code to actually create the login if it does not exist. I was only working with one server in this case so did not bother adding it this time around._

Being that I need to add these objects to each database I start out by getting the collection of databases on the instance:

```powershell
$dbList = $s.Databases
```

From there I am simply going to iterate over each database that will be stored in the variable: `$d`.

### The Meat

The first thing I want to do is verify the database is online and accessible, so each database (e.g. `$d`) has a property called "`isAccessible`" that simply returns `true` or `false`. The equivalent of this in T-SQL would be checking the value of the `status` column in sys.databases. One shortcut you will see in PowerShell at times is the use of an explanation point ( ! ) before an object in the if statement, this basically tells it to check for false to be returned:

```powershell
if (!$d.isAccessible) {...}

#equates to:
if ($d.isAccessible -eq $false) {...}
```

Now that I know the database is online, I need to create and modify some objects in the database. When dealing with objects such as user accounts, roles, tables, etc. in a database, in PowerShell these are going to be classes under the SMO namespace. So in this script I am going to use the following classes for the user and database role:

- <a href="https://msdn.microsoft.com/en-us/library/microsoft.sqlserver.management.smo.user.aspx" target="_blank">Microsoft.SqlServer.Management.Smo.User</a>
- <a href="https://msdn.microsoft.com/en-us/library/microsoft.sqlserver.management.smo.databaserole.aspx" target="_blank">Microsoft.SqlServer.Management.Smo.DatabaseRole</a>

Under the User and Database Role class you will see the <a href="https://en.wikipedia.org/wiki/Constructor_(object-oriented_programming)" target="_blank">constructors</a> section that shows what is needed to create the object. So for example, digging into the link for the database role constructor I see it takes two parameters:

- Microsoft.SqlServer.Management.Smo.Database object
- a string value of what you want to call the role.

The `$d` variable is my database object, so that is covered and then I wrote the function to pass the database role name into the `$roleName`:

```powershell
$r = New-Object Microsoft.SqlServer.Management.Smo.DatabaseRole($d,$roleName)
```

I continued through the article for the database role class and in the Properties list see that some have a description of "Gets the..." and then some have "Gets or sets...". This basically means "Gets the..." = read only property, and "Gets or sets" = property can be read or modified. When you are using CREATE ROLE, via T-SQL, you have to provide the name of the role and the owner of that role. I passed the name of the role when creating the database role object (`$r`) so I just need to set the owner and then call the method to actually create it:

```powershell
$r.Owner = 'dbo' $r.Create();
```

### The Ingredients

The only thing I needed to do in this situation was set INSERT and UPDATE permissions, and at the schema level to handle the client's requirements. Assigning permissions in SMO took me a bit to figure out, majority of the time on writing this script actually. There are two additional classes I need to handle setting permissions on a schema:

- <a href="https://msdn.microsoft.com/en-us/library/microsoft.sqlserver.management.smo.schema.aspx" target="_blank">Microsoft.SqlServer.Management.Smo.Schema</a>
- <a href="https://msdn.microsoft.com/en-us/library/microsoft.sqlserver.management.smo.objectpermissionset.aspx" target="_blank">Microsoft.SqlServer.Management.Smo.ObjectPermissionSet</a>

I create the object for the schema, according to the documented constructor. Within each class that deals with specific objects in a database that can be given access, you should find a `Grant()` method and in my case what I need is <a href="https://msdn.microsoft.com/en-us/library/microsoft.sqlserver.management.smo.schema.grant.aspx" target="_blank">`Grant(ObjectPermissionSet, String[ ])`</a>. The second parameter is an object that contains the permissions I want to assign to this role. This is where the second class above came into play. The properties for the `ObjectPermissionSet` class are the permissions I can assign via SMO to an object in a database, and simply setting them to true will assign that permission:

```powershell
$dboSchema = New-Object Microsoft.SqlServer.Management.Smo.Schema($d,'dbo')
$perms = New-Object Microsoft.SqlServer.Management.Smo.ObjectPermissionSet
$perms.Insert = $true
$perms.Update = $true
$dboSchema.Grant($perms,$roleName);
```

Then to finish it off that last line in the script is to just add the user as a member of the database role created. You can find the full script below for your pleasure. Enjoy!

### Full Script

```powershell
Push-Location
Import-Module SQLPS -DisableNameChecking -NoClobber

function Create-RoleUserInAllDatabases {
<#
	.SYNOPSIS
	Create database role, assign permission, create user, assign user to database role
	.DESCRIPTION
	Iterates through all databases that are online and creates the role and user (if the login exist).
	Assigns INSERT and UPDATE permissions to the role created.
	You can find the other properties that can be set on MSDN site: http://bit.ly/1L9jHhj
	.PARAMETER server
	String. Name of the instance or server (for default instance)
	.PARAMETER loginToUse
	String. Current login on the instance, can be Windows or SQL Login
	.PARAMETER roleName
	Switch. Name of role you want to create.
	.PARAMETER perms
	String. Array, or single, permission you want to assign. **See notes**
	.EXAMPLE
	Create the role AppRole and add "SQLLogin1" as member of that role
	Create-RoleUserInAllDatabaes -server MyServer -loginToUse SQLLogin1 -roleName AppRole
#>
    [cmdletbinding()]
    param (
        [Parameter( Mandatory=$true,ValueFromPipeline=$false )]
        [string]
        $server,

        [string]
        $loginToUse,

        [string]
        $roleName
    )

    $s = New-Object Microsoft.SqlServer.Management.Smo.Server $server

    # Make sure login already exist
    if (!($s.Logins.Contains($loginToUse)))
    {
        Write-Warning "$loginToUse does not exist on $server"
        break;
    }
    $dbList = $s.Databases

    foreach ($d in $dbList) {
        #if databases is not accessible
        if (!$d.isAccessible) {
            Write-Verbose "$($d.Name) is offline"
            contine
        }
        else {
            Write-Verbose "******WORKING ON*****************$d******************"
            # Check if user already exist in database
            if (!($d.Users.Contains($loginToUse))) {
                Write-Verbose "$loginToUse does not exist, creating"
                $u = New-Object Microsoft.SqlServer.Management.Smo.User ($d,$loginToUse)
                $u.Login = $loginToUse
                $u.Create()
            }
            else {
                Write-Verbose "$loginToUse already exist, skipping step"
            }

            # Check if role already exist in database
            if (!($d.Roles.Contains($roleName))) {
                Write-Verbose "$roleName does not exist, creating"
                $r = New-Object Microsoft.SqlServer.Management.Smo.DatabaseRole($d,$roleName)
                $r.Owner = 'dbo'
                $r.Create();
            }
            else {
                Write-Verbose "$roleName already exists, skipping step"
            } #end check if role exist

            # grant permissions
            $dboSchema = New-Object Microsoft.SqlServer.Management.Smo.Schema($d,'dbo')
            $perms = New-Object Microsoft.SqlServer.Management.Smo.ObjectPermissionSet
            $perms.Insert = $true
            $perms.Update = $true
            $dboSchema.Grant($perms,$roleName);

            # now add user
            $r.AddMember($loginToUse);
        } #end check database is online
    } #end foreach $dblist
} #end function
```