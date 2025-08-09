# TCL
TCL:
- Commit
- Rollback
- Save point
- Auto commit mode (set autocommit=0)

DML:
- Insert
- Update
- Delete

1) Start Transaction
2) Execute DMLs:
    - save point a;
    - Query1
    - save point b;
    - Query2
    - save point c;
    - ...
3) Stored to Temp
4) Validate:
    - OK commit;
    - Err roll back;

```sql
select * from AccountDetails;
```
```
+-----------+--------+------+-------------+----------------+
| AccountId | Name   | Age  | AccountType | CurrentBalance |
+-----------+--------+------+-------------+----------------+
|         1 | Ilya   |   21 | Saving      |           1500 |
|         2 | Senya  |   23 | Current     |              0 |
|         3 | John   |   27 | Savings     |              0 |
|         4 | Peter  |   25 | Savings     |              0 |
|         5 | Kirill |   27 | Current     |              0 |
|         6 | Polly  |   32 | Savings     |              0 |
|         7 | Varya  |   28 | Current     |              0 |
|         8 | Sonya  |   24 | Savings     |              0 |
|         9 | Janya  |   22 | Current     |              0 |
|        10 | Jora   |   22 | Current     |              0 |
|        11 | Sema   |   23 | Savings     |              0 |
+-----------+--------+------+-------------+----------------+
```
```sql
set autocommit=0;
start transaction;
delete from AccountDetails where AccountId = 11;
select * from AccountDetails;
```
```
+-----------+--------+------+-------------+----------------+
| AccountId | Name   | Age  | AccountType | CurrentBalance |
+-----------+--------+------+-------------+----------------+
|         1 | Ilya   |   21 | Saving      |           1500 |
|         2 | Senya  |   23 | Current     |              0 |
|         3 | John   |   27 | Savings     |              0 |
|         4 | Peter  |   25 | Savings     |              0 |
|         5 | Kirill |   27 | Current     |              0 |
|         6 | Polly  |   32 | Savings     |              0 |
|         7 | Varya  |   28 | Current     |              0 |
|         8 | Sonya  |   24 | Savings     |              0 |
|         9 | Janya  |   22 | Current     |              0 |
|        10 | Jora   |   22 | Current     |              0 |
+-----------+--------+------+-------------+----------------+
```
```sql
rollback;
select * from AccountDetails;
```
```
+-----------+--------+------+-------------+----------------+
| AccountId | Name   | Age  | AccountType | CurrentBalance |
+-----------+--------+------+-------------+----------------+
|         1 | Ilya   |   21 | Saving      |           1500 |
|         2 | Senya  |   23 | Current     |              0 |
|         3 | John   |   27 | Savings     |              0 |
|         4 | Peter  |   25 | Savings     |              0 |
|         5 | Kirill |   27 | Current     |              0 |
|         6 | Polly  |   32 | Savings     |              0 |
|         7 | Varya  |   28 | Current     |              0 |
|         8 | Sonya  |   24 | Savings     |              0 |
|         9 | Janya  |   22 | Current     |              0 |
|        10 | Jora   |   22 | Current     |              0 |
|        11 | Sema   |   23 | Savings     |              0 |
+-----------+--------+------+-------------+----------------+
```
```sql
commit;
```
# SavePoint
```sql
start transaction;
select * from AccountDetails;
savepoint a;
update AccountDetails set name='Kumi' where AccountId = 2;
savepoint b;
delete from AccountDetails where AccountId=11;
rollback to b;
select * from AccountDetails;
```
```
+-----------+--------+------+-------------+----------------+
| AccountId | Name   | Age  | AccountType | CurrentBalance |
+-----------+--------+------+-------------+----------------+
|         1 | Ilya   |   21 | Saving      |           1500 |
|         2 | Kumi   |   23 | Current     |              0 |
|         3 | John   |   27 | Savings     |              0 |
|         4 | Peter  |   25 | Savings     |              0 |
|         5 | Kirill |   27 | Current     |              0 |
|         6 | Polly  |   32 | Savings     |              0 |
|         7 | Varya  |   28 | Current     |              0 |
|         8 | Sonya  |   24 | Savings     |              0 |
|         9 | Janya  |   22 | Current     |              0 |
|        10 | Jora   |   22 | Current     |              0 |
|        11 | Sema   |   23 | Savings     |              0 |
+-----------+--------+------+-------------+----------------+
```
```sql
rollback to a;
commit;
select * from AccountDetails;
```
```
+-----------+--------+------+-------------+----------------+
| AccountId | Name   | Age  | AccountType | CurrentBalance |
+-----------+--------+------+-------------+----------------+
|         1 | Ilya   |   21 | Saving      |           1500 |
|         2 | Senya  |   23 | Current     |              0 |
|         3 | John   |   27 | Savings     |              0 |
|         4 | Peter  |   25 | Savings     |              0 |
|         5 | Kirill |   27 | Current     |              0 |
|         6 | Polly  |   32 | Savings     |              0 |
|         7 | Varya  |   28 | Current     |              0 |
|         8 | Sonya  |   24 | Savings     |              0 |
|         9 | Janya  |   22 | Current     |              0 |
|        10 | Jora   |   22 | Current     |              0 |
|        11 | Sema   |   23 | Savings     |              0 |
+-----------+--------+------+-------------+----------------+
```
