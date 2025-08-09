# Хранимые процедуры
View имеет ряд недотатков:
- Single Select query
- Update
- Delete
- No parameters
- No variables
- No programming

```sql
DELIMITER //
create procedure BankStatement(Par_AccountId int)
begin
    select * from TransactionDetails where AccountId = Par_AccountId; 
end //
DELIMITER ;

call BankStatement(1);
```
```
+---------------+-----------+-----------------+-------------------+---------------------+
| TransactionId | AccountId | TransactionType | TransactionAmount | TransactionTime     |
+---------------+-----------+-----------------+-------------------+---------------------+
|             1 |         1 | Credit          |              1000 | 2025-08-08 19:56:43 |
|             2 |         1 | Debit           |               500 | 2025-08-08 20:01:57 |
+---------------+-----------+-----------------+-------------------+---------------------+
```
