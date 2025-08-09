# Derived table
Найти n наибольших балансов
```sql
    select CurrentBalance from AccountDetails order by CurrentBalance desc limit 5;
```
```
+----------------+
| CurrentBalance |
+----------------+
|           5500 |
|           5200 |
|           5000 |
|           5000 |
|           2500 |
+----------------+
5 rows in set (0,38 sec)
```
Найти меньший из n наибольших балансов
```sql
select min(CurrentBalance) from AccountDetails where CurrentBalance in
    (select CurrentBalance from AccountDetails order by CurrentBalance desc limit 5);
```
[ERROR 1235 (42000): This version of MySQL doesn't yet support 'LIMIT & IN/ALL/ANY/SOME subquery']

Поэтому:
```sql
select min(CurrentBalance) from
    (select CurrentBalance from AccountDetails order by CurrentBalance desc limit 5) as Top5Balance;
```
```
+---------------------+
| min(CurrentBalance) |
+---------------------+
|                2500 |
+---------------------+

```

```sql
select max(CurrentBalance) from AccountDetails where CurrentBalance not in
    (select max(CurrentBalance) from AccountDetails where CurrentBalance not in
        (select max(CurrentBalance) from AccountDetails));
```
```
+---------------------+
| max(CurrentBalance) |
+---------------------+
|                5500 |
+---------------------+
```
