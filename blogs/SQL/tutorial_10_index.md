# SQL index
Add index will increase SELECT performance.

InnoDB default index is BTREE stored.

SQL syntax of new index:

```sql
CREATE [UNIQUE|FULLTEXT|SPATIAL] INDEX index_name
[USING index_type]
ON tbl_name (index_col_name, ...)

index_col_name:
    col_name[(length)][ASC|DESC]
```

e.g.
```sql
CREATE INDEX first_name ON user(first_name(10));
```

SQL syntax of remove index:
```sql
DROP INDEX index_name ON tbl_name;
```
---
## General rule
* Best for column in WHERE clause.
* The more unique, the better.
* The shorter, the better.
* ~~Not understand~~
* No overuse index.
* Optimize primary index first.
---
## BTREE vs HASH
* HASH index available when use = OR <=> to compare (include IN clause).
* HASH can search one row.
* BTREE index always available.
* 