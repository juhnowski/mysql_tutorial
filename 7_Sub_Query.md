# Подзапросы
Это запрсы внутри которых другие запросы.
внутренний запрос будет выполнен перед where/having
## Подготовка
```sql
insert into AccountDetails values (2,'Senya',23,'Current',500),
    (3,'John',27,'Savings',1000), 
    (4,'Peter',25,'Savings',1500),
    (5,'Kirill',27,'Current',5200),
    (6,'Polly',32,'Savings',5500),
    (7,'Varya',28,'Current',500),
    (8,'Sonya',24,'Savings',2500),
    (9,'Janya',22,'Current',5000),
    (10,'Jora',22,'Current',5000),
    (11,'Sema',23,'Savings',1500);

select * from AccountDetails;
```

```
+-----------+--------+------+-------------+----------------+
| AccountId | Name   | Age  | AccountType | CurrentBalance |
+-----------+--------+------+-------------+----------------+
|         1 | Ilya   |   21 | Saving      |           1000 |
|         2 | Senya  |   23 | Current     |            500 |
|         3 | John   |   27 | Savings     |           1000 |
|         4 | Peter  |   25 | Savings     |           1500 |
|         5 | Kirill |   27 | Current     |           5200 |
|         6 | Polly  |   32 | Savings     |           5500 |
|         7 | Varya  |   28 | Current     |            500 |
|         8 | Sonya  |   24 | Savings     |           2500 |
|         9 | Janya  |   22 | Current     |           5000 |
|        10 | Jora   |   22 | Current     |           5000 |
|        11 | Sema   |   23 | Savings     |           1500 |
+-----------+--------+------+-------------+----------------+
11 rows in set (0,00 sec)
```
```sql
insert into TransactionDetails (AccountId, TransactionType, TransactionAmount) values (7, 'Credit',1000);
select * from TransactionDetails;
```
```
+---------------+-----------+-----------------+-------------------+---------------------+
| TransactionId | AccountId | TransactionType | TransactionAmount | TransactionTime     |
+---------------+-----------+-----------------+-------------------+---------------------+
|             1 |         1 | Credit          |              1000 | 2025-08-08 19:56:43 |
|             2 |         1 | Debit           |               500 | 2025-08-08 20:01:57 |
|             3 |         7 | Credit          |              1000 | 2025-08-08 23:59:48 |
+---------------+-----------+-----------------+-------------------+---------------------+
```
## Задача: Получить AccountDetails для людей с транзакциями
### Решение вручную

```sql
select DISTINCT(AccountId) from TransactionDetails; 
```
```
+-----------+
| AccountId |
+-----------+
|         1 |
|         7 |
+-----------+
```

```sql
select * from AccountDetails where AccountId in (1,7);
```
+-----------+-------+------+-------------+----------------+
| AccountId | Name  | Age  | AccountType | CurrentBalance |
+-----------+-------+------+-------------+----------------+
|         1 | Ilya  |   21 | Saving      |           1000 |
|         7 | Varya |   28 | Current     |            500 |
+-----------+-------+------+-------------+----------------+

## Одним запросом
```sql
select * from AccountDetails where AccountId in (
    select DISTINCT(AccountId) from TransactionDetails
);
```
