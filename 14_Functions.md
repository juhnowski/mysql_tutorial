# Функции
В SQL существуют функции, которые позволяют выполнять операции над данными в запросах. Они делятся на два основных типа: скалярные и агрегатные. Скалярные функции обрабатывают каждое значение по отдельности, возвращая одно значение, в то время как агрегатные функции обрабатывают набор значений и возвращают одно агрегированное значение.
- system defined functions (sum,min,maks,avg)
- user defined functions

```sql
set global log_bin_trust_function_creators = 1;
drop function AgeCalculator;


DELIMITER //
create function AgeCalculator (Par_DateOfBirth date)
returns tinyint
begin
    declare Var_age tinyint;
    select timestampdiff(year,Par_DateOfBirth,now()) into Var_age;
    return Var_Age;
end //
DELIMITER ;

select AgeCalculator('1978-11-29'); 
```
```
+-----------------------------+
| AgeCalculator('1978-11-29') |
+-----------------------------+
|                          46 |
+-----------------------------+
```
