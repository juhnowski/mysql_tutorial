# SQL Команды
## Языки команд:
- DDL - Data Definition Language
    - Create - создает
        - Database ```sql create database dbname;```
        - Table ```sql create table tname;```
        - DB Objects ```sql create view vname;```
    - Alter+Rename - модифицирует структуру таблицы или объектов БД
        - Add column - добавить колонку к существующей таблице
        - Reove column - удалить колонку из существующей таблицы
    - Drop - удаляет 
        - таблицу из БД
        - БД из РСУБД
    - Truncate - удаляет все существующие записи в таблице за один раз и за один шаг
- DML - Data Manipulation Language
- DQL - Data Query Language
- TCL - Transaction Control Language
- DCL - Data Control Language
## Data Types
- Number
    - Integer
        - TinyInt: 1 байт = 8 бит, 2^n-1=254
        - SmallInt: 2 байта = -32768 до 32767 (32КБ)
        - Int: 4 байта =  от -2,147,483,648 до 2,147,483,647, а для беззнакового - от 0 до 4,294,967,295
        - BigInt: 8 байт = 2^64-1
    - Fractional
        - Float: 16 digits
        - Double:  32 digits
        - Decimal: 32 digits
    - Text
        - char
        - varchar
        - text
    - DateTime
## Практика
```sql
create database StudentDB;
use StudentDB;
create table StudentDetails (
    Id int,
    Name char(20),
    Age tinyint,
    Gender varchar(10)
);

select * from StudentDetails;
insert into StudentDetails values (1, 'Ram', 21, 'Male');
insert into StudentDetails values (2, 'Sita',20,'Female'), (3,'Gita',20,'Female');
insert into StudentDetails (id,name,gender)  values (4, 'Ramo',  'Male');
update StudentDetails set name='Ilya' where id = 1;
set sql_safe_updates=0;
drop table StudentDetails;
```
safety warning error

## Delete
    - Single record
    - Multiple record
    - All records
    - Undo; - откатывает удаление используя Transaction Control Language
```sql
delete from StudentDetails where id=1;
delete from StudentDetails where id in (1,2,3);
delete from StudentDetails;
truncate table StudentDetails;

alter table StudentDetails add Location varchar(20);
insert into StudentDetails values (1, 'Ram', 21, 'Male','NN');
insert into StudentDetails values (2, 'Sita',20,'Female','SPB'), (3,'Gita',20,'Female','SPB');

update StudentDetails set location='India';
```
