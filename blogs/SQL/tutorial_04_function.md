# String functions:
## CONCAT(S1, S2,...,Sn)
```sql
SELECT CONCAT('ab', 'cd', 'ef'), CONCAT('A', null);
```
## INSERT(str, x, y, in_str)
```sql
SELECT INSERT('abcdefg', 1, 0, 'zzz');
SELECT INSERT('abcdefg', 1, 2, 'zzz');
SELECT INSERT('abcdefg', 2, 2, 'zzz');
```
## LOWER(str) UPPER(str);
```sql
SELECT LOWER('ABCdef'), UPPER('ABCdef');
```
## LEFT(str, x) RIGHT(str, x)
```sql
SELECT LEFT('ABCdef', 3), RIGHT('ABCdef', 3), LEFT('ASDF', NULL);
```
## LPAD(str, n, pad) RPAD(str, n, pad)
```sql
SELECT LPAD('ABCdef', 3, '*'), RPAD('ABCdef', 3, '*');
SELECT LPAD('ABCdef', 10, '*'), RPAD('ABCdef', 10, '*');
```
## TRIM(str) LTRIM(str) RTRIM(str)
```sql
SELECT 
'   dsf   ' Original, 
TRIM('   dsf   ') T, 
LTRIM('   dsf   ') LT, 
RTRIM('   dsf   ') RT;
```
## REPEAT(str, x)
```sql
SELECT REPEAT('ABC', 3);
```
## REPLACE(str, a, b)
```sql
SELECT REPLACE('ABCAdef', 'A', '*');
```
## STRCMP(s1, s2)
```sql
SELECT STRCMP('ABC', 'DEF'), STRCMP('B', 'A'), STRCMP('A', 'A');
```
## SUBSTRING(str, x, y)
```sql
SELECT SUBSTRING('ABCdef', 1, 2);
```

# Numerical functions:

## ABS(x)
```sql
SELECT ABS(0.5), ABS(-0.5);
```
## CEIL(x)
```sql
SELECT CEIL(1.2), CEIL(-1.2);
```
## FLOOR(x)
```sql
SELECT FLOOR(1.2), FLOOR(-1.2);
```
## MOD(x, y)
## RAND()
```sql
SELECT RAND(), RAND();
SELECT CEIL(100*RAND());
```
## ROUND(x, y) TRUNCATE(x, y)
```sql
SELECT ROUND(1.46), ROUND(1.46, 1), ROUND(1.46, 4);
SELECT ROUND(1.46, 1), TRUNCATE(1.46, 1);
```

# Date and time functions:

## CURDATE() CURTIME() NOW()
```sql
SELECT CURDATE(), CURTIME(), NOW();
```
## UNIX_TIMESTAMP(date) FROM_UNIXTIME(unix_time)
```sql
SELECT UNIX_TIMESTAMP(CURDATE()), UNIX_TIMESTAMP(NOW());
SELECT FROM_UNIXTIME(UNIX_TIMESTAMP(NOW()));
```
## WEEK(date) YEAR(date) MONTHNAME(date)
```sql
SELECT WEEK(NOW()), YEAR(NOW()), MONTHNAME(NOW());
```
## HOUR(time) MINUTE(time)
```sql
SELECT NOW(), HOUR(NOW()), MINUTE(NOW());
```
## DATE_FORMAT(date, fmt)
```sql
SELECT DATE_FORMAT(NOW(), '%M,%D,%Y');
```
## DATE_ADD(date, INTERVAL expr type)
```sql
SELECT 
NOW(), 
DATE_ADD(NOW(), INTERVAL 10 DAY) '10 days later', 
DATE_ADD(NOW(), INTERVAL 3 MONTH) '3 month later';
```
## DATEDIFF(expr, expr2)
```sql
SELECT DATEDIFF('2019-8-4', NOW());
```

# Conditional function

## IF(value, t, f)
```sql
SELECT first_name, last_name, age, IF(age>25, 'old', 'young') FROM user;
```
## IFNULL(value1, value2)
## CASE WHEN [condition1] THEN [result1] ... ELSE [DEFAULT] END
```sql
SELECT age, CASE WHEN age>25 THEN 'old' ELSE 'young' END FROM user;
```
## CASE [expr] WHEN [value1] THEN [result1] ... ELSE [DEFAULT] END
```sql
SELECT age, CASE age WHEN 26 THEN 'young' WHEN 27 THEN 'mid' ELSE 'old' END FROM user;
```
# Other functions

## DATABASE() VERSION() USER()
```sql
SELECT DATABASE(), VERSION(), USER();
```
## INET_ATON(IP) INET_NTOA(NUM)
```sql
SELECT INET_ATON('172.17.0.1'), INET_NTOA(2886795265);
```
## PASSWORD(str) MD5(str)
```sql
SELECT PASSWORD('hello'), MD5('hello');
```

