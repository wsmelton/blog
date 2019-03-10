---
title: SQL Server Maintenance Plan Logging
date: 2014-12-08T08:00:00-06:00
drafts: false
---

Whether you are an advocate of Maintenance Plans or not, they have their place in some situations. However, when you do use them there is one thing you should understand that is turned on by default with every maintenance plan you create: **report and logging**. I am not sure why, but Microsoft decided that any sub-plan that exist within a maintenance plan should have a log created for it by date.

I have lost count of how many times I come across servers and review their default log directory to find thousands of small text files from years back of maintenance plan logs. How large the files are is based on what actions are being performed within the sub-plan of the maintenance plan.

You will generally find the log directory with files that are similar to this:

![](/images/maintenanceplanreportfiles1.png)

Now to see how this is configured if you open up a maintenance plan you will find a button on the top of that window pane to open up the reporting setup:

![](/images/maintenanceplan_reportloggingsetup.png)

![](/images/maintenanceplan_reportloggingsetup2.png)

I will on every occasion simply uncheck the box for "Generate a test file report" because I do not need hundreds of files created that are simply going to show "successful" attempts:

![](/images/maintenanceplanreportfile.png)

If my maintenance plan is failing I will just use the output file that is configured on a SQL Agent job step, under the Advanced page. There, by default, it will do the one thing you can't have the report and logging in maintenance plan do: overwrite my log file each time. I only need one log file to check in the event something failed.

![](/images/maintenanceplan_sqlagentstepoutputconfig.png)
