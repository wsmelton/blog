---
title: To the future…
date: 2013-10-17T10:00:00-06:00
draft: false
---

I decided to jump into playing with Windows Azure today. I heard on Twitter yesterday that Azure had SQL Server 2014 CTP2 available. After waiting about 30 minutes I was able to login and see this:

![](/img/azure_sql2014.png)

Well the first thing I wanted to check out was the SQLPS module. Fired up PowerShell and fired off this command: `Import-Module SQLPS –Verbose`

After which I ran the following command, to get a full list of “cmdlets” that are available:
`Get-Command -Module SQLPS | Out-GridView`

This will give you a nice list of commands to start getting familiar with:
<table style="border-collapse:collapse;" width="461" border="0" cellspacing="0" cellpadding="0"><col style="width:76pt;" width="101" /> <col style="width:200pt;" width="267" /> <col style="width:70pt;" width="93" />
<tbody>
<tr style="height:15pt;">
<td class="xl65" style="vertical-align:bottom;padding-top:1px;padding-left:1px;padding-right:1px;border:windowtext .5pt solid;" width="101" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;"><strong>CommandType</strong></span></span></td>
<td class="xl65" style="border-top:windowtext .5pt solid;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;" width="266"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;"><strong>Name</strong></span></span></td>
<td class="xl65" style="border-top:windowtext .5pt solid;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;" width="93"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;"><strong>ModuleName</strong></span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Function</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLSERVER:</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Add-SqlAvailabilityDatabase</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Add-SqlAvailabilityGroupListenerStaticIp</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Add-SqlFirewallRule</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Backup-SqlDatabase</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Convert-UrnToPath</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Decode-SqlName</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Disable-SqlAlwaysOn</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Enable-SqlAlwaysOn</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Encode-SqlName</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Get-SqlCredential</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Get-SqlDatabase</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Get-SqlInstance</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Get-SqlSmartAdmin</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Invoke-PolicyEvaluation</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Invoke-Sqlcmd</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Join-SqlAvailabilityGroup</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">New-SqlAvailabilityGroup</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">New-SqlAvailabilityGroupListener</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">New-SqlAvailabilityReplica</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">New-SqlBackupEncryptionOption</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">New-SqlCredential</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">New-SqlHADREndpoint</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Remove-SqlAvailabilityDatabase</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Remove-SqlAvailabilityGroup</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Remove-SqlAvailabilityReplica</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Remove-SqlCredential</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Remove-SqlFirewallRule</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Restore-SqlDatabase</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Resume-SqlAvailabilityDatabase</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Set-SqlAuthenticationMode</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Set-SqlAvailabilityGroup</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Set-SqlAvailabilityGroupListener</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Set-SqlAvailabilityReplica</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Set-SqlCredential</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Set-SqlHADREndpoint</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Set-SqlNetworkConfiguration</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Set-SqlSmartAdmin</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Start-SqlInstance</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Stop-SqlInstance</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Suspend-SqlAvailabilityDatabase</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Switch-SqlAvailabilityGroup</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Test-SqlAvailabilityGroup</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Test-SqlAvailabilityReplica</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Test-SqlDatabaseReplicaState</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
<tr style="height:15pt;">
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:windowtext .5pt solid;padding-right:1px;" height="20"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Cmdlet</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">Test-SqlSmartAdmin</span></span></td>
<td class="xl66" style="border-top:medium none;border-right:windowtext .5pt solid;vertical-align:bottom;border-bottom:windowtext .5pt solid;padding-top:1px;padding-left:1px;border-left:medium none;padding-right:1px;"><span style="font-family:Calibri;"><span style="color:#000000;font-size:11pt;">SQLPS</span></span></td>
</tr>
</tbody>
</table>
Now go forth and conquer.
