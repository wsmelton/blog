---
title: SQL Server Activity Monitor Script
date: 2014-07-30T13:00:00-06:00
drafts: false
tags: [sqlserver]
---

You ever wonder what goes in the background of Activity Monitor? Me neither, I just used it every so often when I wanted a quick peek at what was going on for a server. Microsoft has actually made changes to Activity Monitor in SQL Server 2012 Service Pack 1 that can cause errors, and requires you to modify OS level permissions, [reference]("http://blogs.msdn.com/b/sqlagent/archive/2013/02/07/activity-monitor-in-sql-server-2012-sp1.aspx"). I work over VPN supporting clients remotely and it never been that useful to me.

I liked all the information it showed but just did not like having to use the UI it provided to filter and such. So I did a trace against an instance while I opened Activity Monitor to pull out what query it was running to populate the active sessions.

So this post is pretty much just a bookmark for the script:

```sql
SELECT [Session ID] = s.session_id
	,[User Process] = CONVERT(CHAR(1), s.is_user_process)
	,[Login] = s.login_name
	,[Database] = ISNULL(db_name(p.dbid), N'')
	,[Task State] = ISNULL(t.task_state, N'')
	,[Command] = ISNULL(r.command, N'')
	,[Application] = ISNULL(s.program_name, N'')
	,[Wait Time (ms)] = ISNULL(w.wait_duration_ms, 0)
	,[Wait Type] = ISNULL(w.wait_type, N'')
	,[Wait Resource] = ISNULL(w.resource_description, N'')
	,[Blocked By] = ISNULL(CONVERT(VARCHAR, w.blocking_session_id), '')
	,[Head Blocker] = CASE
		WHEN r2.session_id IS NOT NULL
			AND (
				r.blocking_session_id = 0
				OR r.session_id IS NULL
				)
			THEN '1'
		ELSE ''
		END
	,[Total CPU (ms)] = s.cpu_time
	,[Total Physical I/O (MB)] = (s.reads + s.writes) * 8 / 1024
	,[Memory Use (KB)] = s.memory_usage * 8192 / 1024
	,[Open Transactions] = ISNULL(r.open_transaction_count, 0)
	,[Login Time] = s.login_time
	,[Last Request Start Time] = s.last_request_start_time
	,[Host Name] = ISNULL(s.host_name, N'')
	,[Net Address] = ISNULL(c.client_net_address, N'')
	,[Execution Context ID] = ISNULL(t.exec_context_id, 0)
	,[Request ID] = ISNULL(r.request_id, 0)
	,[Workload Group] = N''
FROM sys.dm_exec_sessions s
LEFT JOIN sys.dm_exec_connections c ON (s.session_id = c.session_id)
LEFT JOIN sys.dm_exec_requests r ON (s.session_id = r.session_id)
LEFT JOIN sys.dm_os_tasks t ON (
		r.session_id = t.session_id
		AND r.request_id = t.request_id
		)
LEFT JOIN (
	SELECT *
		,ROW_NUMBER() OVER (
			PARTITION BY waiting_task_address <br />			ORDER BY wait_duration_ms DESC
			) AS row_num
	FROM sys.dm_os_waiting_tasks
	) w ON (t.task_address = w.waiting_task_address)
	AND w.row_num = 1
LEFT JOIN sys.dm_exec_requests r2 ON (s.session_id = r2.blocking_session_id)
LEFT JOIN sys.sysprocesses p ON (s.session_id = p.spid)
WHERE s.is_user_process = 1
ORDER BY s.session_id;
```
