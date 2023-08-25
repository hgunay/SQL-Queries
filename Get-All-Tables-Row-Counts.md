Get table row counts

```sql
SELECT
	 SCHEMA_NAME(schema_id)		AS [SchemaName]
	,[Tables].name				AS [TableName]
	,SUM([Partitions].[rows])	AS [TotalRowCount]
FROM 
	sys.tables AS [Tables]
JOIN sys.partitions AS [Partitions] ON [Tables].[object_id] = [Partitions].[object_id]
    AND [Partitions].index_id IN ( 0, 1 )
-- WHERE [Tables].name LIKE N'%TABLE_NAME%'
GROUP BY 
	SCHEMA_NAME(schema_id), [Tables].name
ORDER BY 
	[TotalRowCount] DESC
```

Result

| SchemaName  |	TableName	                      | TotalRowCount |
|------       |-------------                    |:-------=:|
| dbo	        | NCM_Audit	                      | 31114319 |
| dbo	        | NetFlowFastBitStringHeap	      | 27764990 |
| dbo	        | APM_ComponentStatus_Detail	    | 18809768 |
| dbo	        | APM_PortEvidence_Detail	        | 17968995 |
| dbo	        | ContainerStatus_HourlyData	    | 13092972 |
| dbo	        | ContainerStatus_Hourly	        | 13064259 |
| dbo	        | ResponseTime_CS_Detail_20230819	| 12176695 |
| dbo	        | ResponseTime_CS_Detail_20230820	| 12078000 |
| dbo	        | ResponseTime_CS_Detail_20230823	| 11699163 |
| dbo	        | ResponseTime_CS_Detail_20230821	| 11607593 |
