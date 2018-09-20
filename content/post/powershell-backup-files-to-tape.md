---
title: Backup Files to Tape
date: 2014-10-28T08:00:00-06:00
drafts: false
tags: [powershell]
---

I had a maintenance plan on a server with a client that was having issues running successfully each night because it ended up filling the drive. This as it turns out ended up being that the clean up task was set to delete backups older than 1 day. Ok you would think that was sufficient, however it appears in this instance that was not working. The time stamps showing for the previous day backup was within a minute of the next run of the maintenance plan. So I took it to mean that it was not actually seeing them as over a day old and therefore skipped them. I decided to change it to 21 hours instead of one day and that seemed to work for this client.

Either way I needed to delete the old backups that I know were already backed up to tape. To do this I wrote up this function that will simply return a bit of information on the file like name, last access, last write, and attribute values. The attribute will show "Normal" if the file has been backed up (or the archive bit cleared) and "Archive" if it still has to be backed up.

**Now I would caution you to do your own verification as to whether the file actually exist on your backup media (tape, disk, etc.).** There are multiple things that can modify the archive bit, so use at your own discretion.

```powershell
function Verify-FileBackedUp ($rootdir,[switch]$recurse)
{
  # if value "archive" is shown means file has not been backed up
  # if value "normal" is shown means file has been backed up, or the archive bit cleared
  if ($recurse)
  {
    dir $rootdir -recurse | where {-not $_.PSIsContainer} | select FullName, LastAccessTime, LastWriteTime,
      @{Label="FileBackedUp";Expression={(Get-ItemProperty $_.FullName).Attributes}}
  }
  else
  {
    dir $rootdir | where {-not $_.PSIsContainer} |
      select FullName, LastAccessTime, LastWriteTime,
      @{Label="FileBackedUp";Expression={(Get-ItemProperty$_.FullName).Attributes}
  }
}
```

A sample output would look something like below:

![](/img/verify_filebackup.png)
