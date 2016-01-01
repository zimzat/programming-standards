
## Database Query Standards

* All keywords must be in uppercase.
* Boolean values should omit equality comparison.
* ON clauses should place the immediately joined table as the left hand side of the comparison.
* Queries which contain more than one table must use short aliases for all tables.
* Short and simple queries may use a single line or may be expanded.
* Queries that contain more than one or two SELECT columns, one or two WHERE clauses, or any JOINs must be split onto multiple lines.

Examples:

```sql
SELECT * FROM someTable WHERE isEnabled AND NOT isDeleted
```

```sql
SELECT *
FROM anotherTable
WHERE NOT isEnabled
	AND isDeleted
```

```sql
SELECT
	a.fieldA,
	b.fieldB,
	c.fieldC,
	w.fieldW
FROM Apple AS a
	JOIN Banana AS b ON (b.bananaId = a.bananaId)
	JOIN Carrot AS c ON (c.carrotId = a.carrotId)
	LEFT JOIN Watermelon AS w ON (
		w.watermelonId = a.watermelonId
		AND w.isRipe
		AND w.isWhole
	)
WHERE a.isRipe
	AND (
		a.color IN ('red', 'green')
		OR a.taste = 'sweet'
	)
```

