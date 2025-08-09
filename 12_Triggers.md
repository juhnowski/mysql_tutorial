# Тригеры нужны для автоматизации запросов
- выполнются автоматически
- не выводят resultset

```sql
DELIMITER //
create trigger TriggerName Before/After insert/update/delete on TableName for each row
begin

end
DELIMITER ;
```

```sql
truncate table TransactionDetails;
update AccountDetails set CurrentBalance = 0;
drop trigger BalanceUpdater;

DELIMITER //
create trigger BalanceUpdater after insert on TransactionDetails for each row
begin
    declare Var_LatestTransactionId int;
    declare Var_AccountId int;
    declare Var_TransactionType varchar(10);
    declare Var_TransactionAmount int;
    declare Var_CurrentBalance int;

    select max(TransactionId) into Var_LatestTransactionId from TransactionDetails;

    select AccountId,TransactionType,TransactionAmount into  Var_AccountId, Var_TransactionType, Var_TransactionAmount
        from TransactionDetails where TransactionId = Var_LatestTransactionId;
    
    select CurrentBalance into Var_CurrentBalance from AccountDetails where AccountId = Var_AccountId; 


    if Var_TransactionType='Credit' then
        if Var_TransactionAmount <= Var_CurrentBalance then
            update AccountDetails set CurrentBalance = CurrentBalance - Var_TransactionAmount where AccountId = Var_AccountId;
        end if;
    else
        update AccountDetails set CurrentBalance = CurrentBalance + Var_TransactionAmount where AccountId = Var_AccountId;
    end if;
end //
DELIMITER ;

insert into TransactionDetails(AccountId, TransactionType, TransactionAmount) values (1,'Debit',1000);
insert into TransactionDetails(AccountId, TransactionType, TransactionAmount) values (1,'Credit',500);
select * from TransactionDetails;
select * AccountDetails;
```
```
+---------------+-----------+-----------------+-------------------+---------------------+
| TransactionId | AccountId | TransactionType | TransactionAmount | TransactionTime     |
+---------------+-----------+-----------------+-------------------+---------------------+
|             1 |         1 | Credit          |              1000 | 2025-08-09 17:48:46 |
+---------------+-----------+-----------------+-------------------+---------------------+
```
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
