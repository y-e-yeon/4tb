### 강의를 마치며 학습 내용 전체 총 정리

**BigQuery Query 문 구조**

```sql
WITH CTE AS (
	SELECT
		col,
		col2,
	FROM Table
)
SELECT
	a.col3,
	b.col4,
	COUNT(DISTINCT a.id) AS cnt
FROM table_a AS a
LEFT JOIN table_b AS b
ON a.id = b.id
WHERE
	a.col3 >= 3
GROUP BY
	a.col3,
	b.col4
HAVING
	cnt >= 2
ORDER BY cnt DESC
LIMIT 10
```

![image.png](../SQL/image/Section_9/마치며.png)