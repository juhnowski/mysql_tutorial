# View
create view ViewName as Query;
- updatable views
- unapdatable views 
```sql
create view AccountsOfTransactions as
    select * from AccountDetails where AccountId in
    (select distinct(AccountId) from TransactionDetails);

select * from AccountsOfTransactions;
```
```
+-----------+-------+------+-------------+----------------+
| AccountId | Name  | Age  | AccountType | CurrentBalance |
+-----------+-------+------+-------------+----------------+
|         1 | Ilya  |   21 | Saving      |           1000 |
|         7 | Varya |   28 | Current     |            500 |
+-----------+-------+------+-------------+----------------+
```

```sql
create view BalanceInBank as
    select sum(CurrentBalance) from AccountDetails;

select * from BalanceInBank;
```

```
+---------------------+
| sum(CurrentBalance) |
+---------------------+
|               29200 |
+---------------------+
```
