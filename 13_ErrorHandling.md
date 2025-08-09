# Обработка ошибок
MySQL error code 1146, commonly presented as "Table 'database-name.table-name' doesn't exist," indicates that the MySQL server cannot find a table referenced in a query or operation within the specified database.

```sql
DELIMITER //

declare VariableName int/char;
declare continue handler for 1146
begin
    select 'please cheek Table Name' as msg;
end //
DELIMITER ;
```
## Пример
```sql
DELIMITER //
create procedure ErrorHandler()
begin
    declare continue handler for 1146
    begin
        select 'Check Your Table Name' as Msg;
    end;
    select * from AcDetails;
end //

DELIMITER ;

call ErrorHandler();
```
```
+-----------------------+
| Msg                   |
+-----------------------+
| Check Your Table Name |
+-----------------------+
```
