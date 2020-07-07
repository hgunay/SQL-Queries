```sql
WITH CTE AS (
    SELECT 
        [COLUMN_NAME]
        ROW_NUMBER() OVER (
            PARTITION BY 
                [COLUMN_NAME]
            ORDER BY 
                [COLUMN_NAME]
        ) ROW_NUM
     FROM 
        [TABLE_NAME]
)
DELETE FROM CTE WHERE ROW_NUM > 1
SELECT * FROM CTE WHERE ROW_NUM > 1
```

Örnek Kod;
```sql
WITH CTE AS (
    SELECT 
         Name
		    ,Description
        ,ROW_NUMBER() 
		    OVER (
            PARTITION BY
               Name
              ,Description
            ORDER BY
               Name
              ,Description
        ) ROW_NUM
     FROM  [Project]
)
SELECT * FROM CTE WHERE ROW_NUM > 1
```
Sonuç;

| Name        | Description               | ROW_NUM |
|------       |-------------              |:-------:|
|Test Project |	Test Project Description  |	2       |

Silme İşlemi;
```sql
WITH CTE AS (
    SELECT 
         Name
		    ,Description
        ,ROW_NUMBER() 
		    OVER (
            PARTITION BY
               Name
              ,Description
            ORDER BY
               Name
              ,Description
        ) ROW_NUM
     FROM  [Project]
)
DELETE FROM CTE WHERE ROW_NUM > 1
```
