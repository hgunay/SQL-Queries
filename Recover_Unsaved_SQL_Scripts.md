```sql
USE <database>
SELECT 
   EXQ.last_execution_time  AS ExecDateTime
  ,EXS.text                 AS RunnedScript 
FROM 
  sys.dm_exec_query_stats AS EXQ
CROSS APPLY sys.dm_exec_sql_text(EXQ.sql_handle) AS EXS
WHERE 
  EXS.text LIKE '%<search_text>%'
ORDER BY
  EXQ.last_execution_time DESC
```

Örnek Kod;
```sql
USE Sample_DB
SELECT 
   EXQ.last_execution_time  AS ExecDateTime
  ,EXS.text                 AS RunnedScript 
FROM 
  sys.dm_exec_query_stats AS EXQ
CROSS APPLY sys.dm_exec_sql_text(EXQ.sql_handle) AS EXS
WHERE 
  EXS.text LIKE '%ProjectDetail%'
ORDER BY
  EXQ.last_execution_time DESC
```
