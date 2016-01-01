
## Database Query Standards

* All keywords must be in uppercase.
* Boolean values should omit equality comparison.
* JOIN conditions should place the immediately joined table as the left hand side of the comparison.
* JOIN conditions containing only one comparison may be placed on the same line as the JOIN, otherwise must be split onto multiple lines and indented.
* Queries must not use commas to include multiple tables.
* All conditions which reference two tables should be placed in the ON instead of WHERE.
* Queries which contain more than one table must use short aliases for all tables.
* Short and simple queries may use a single line or may be expanded.
* Queries that contain more than one or two SELECT columns, one or two WHERE clauses, or any JOINs must be split onto multiple lines.

Examples:

```sql
SELECT * FROM someTable WHERE isEnabled AND !isDeleted
```

```sql
SELECT *
FROM anotherTable
WHERE !isEnabled
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

