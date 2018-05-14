---
title: Create-ServerDirectory
date: 2013-10-30T11:00:00-06:00
draft: false
---

If you have to do it more than once, script it and blog about it…

```powershell
function Create-ServerDirectory
{
    [CmdletBinding()]
    Param
    (
        # server name or instance name of SQL Server to run assessment against
        [Parameter(Mandatory=$true,Position=0)]
        [ValidateNotNull()]
        [ValidateNotNullOrEmpty()]
        [string]$location,

        [Parameter(Mandatory=$true,Position=1,
            ValueFromPipeline=$true,
            HelpMessage='Provide a single or comma separated list of server names.' )]
        [ValidateNotNull()]
        [ValidateNotNullOrEmpty()]
        [string[]]$server
    )

    foreach ($s in $server) {
        $dirName = $s.Replace("\","_")
        $fullPath = "$location\$dirName"
        if(Test-Path $fullPath) {
            Write-Warning "The path $fullPath already exist"
        }
        else {
            New-Item -Path $fullPath -ItemType Directory | Out-Null
            if(Test-Path $fullPath){
                Write-Host "$fullPath created successfully"
            }
            else {
                Write-Warning "Some issue occurred creating the directory"
            }
        }
    }
}
```

So a few examples:

```powershell
Create-ServerDirectory –location c:\temp –server "Server1","Server2","Server1\Instance1","Server3"

#OR

$list = “Server1”,”Server2”,”Server1\Instance1”,”Server3”
Create-ServerDirectory –location c:\temp –server $list

#OR

"Some cmdlet that passes your server name down pipeline" | foreach {Create-ServerDirectory –location c:\temp –server $_}
```

Carry on…