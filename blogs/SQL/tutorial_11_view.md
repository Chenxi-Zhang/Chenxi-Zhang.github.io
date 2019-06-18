# View
SQL syntax: create view:
```sql
CREATE [OR REPLACE] [ALGORITHM = {UNDEFINED | MERGE | TEMPTABLE}]
    VIEW view_name [(column_list)]
    AS select_statement
    [WITH [CASCADED|LOCAL] CHECK OPTION]
```
Alter view:
```sql
ALTER [ALGORITHM = {UNDEFINED | MERGE | TEMPTABLE}]
    VIEW view_name [(column_list)]
    AS select_statement
    [WITH [CASCADED|LOCAL] CHECK OPTION]
```
e.g.
```sql
CREATE OR REPLACE VIEW user_permission_view
AS SELECT user.id, user.first_name, user.last_name, p.publish
FROM user, permission_group p WHERE user.permission_group=p.name;
```

Delete view:
```sql
DROP VIEW [IF EXISTS] view_name [,view_name2 ...] [RESTRICT|CASCADE]