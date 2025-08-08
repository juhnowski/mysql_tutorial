# Business Integrity - это как мы чисто и аккуратно обрабатываем/сохраняем данные
Реализуем с помощью ограничений Constraints
- Regular Constraints
    - Null - unknown value, (не равен 0), если имя должно быть всегда (обязательно), то пишем notNull
    - Default - пишем значение по умолчанию
    - Check - проверяем условия, например Age>18
- Key Constraints: ключ это значение (value), которое используется для поиска персоны, объекта, транзакции. Если ты персона, то ты долженполучить свои данные, не чьи другие.
    - Unique - не должно дублироваться, но разрешает одну запись с Null значением
    - PrimaryKey - это комбинация Unique NotNull, может быть одно на таблицу (Parent)
    - ForeignKey - используется для построение Referential Integrity         (Child)
    - AutoIncrement - генерирует последовательность значений 1,2,3,4...

## Пример ненормализованной таблицы
```sql
create table NN (sid int, name char(20), Age int, cid int, cname char(20), fee char(10));
insert into NN values (1,'Ram',21,1,'SQL','15k');
insert into NN values (2,'Sana',23,1,'SQL','15k');
insert into NN values (3,'John',27,2,'PowerBI','12k');
insert into NN values (4,'Peter',24,2,'PowerBI','12k');
select * from NN;
```
```pseudographics
+------+-------+------+------+---------+------+
| sid  | name  | Age  | cid  | cname   | fee  |
+------+-------+------+------+---------+------+
|    1 | Ram   |   21 |    1 | SQL     | 15k  |
|    2 | Sana  |   23 |    1 | SQL     | 15k  |
|    3 | John  |   27 |    2 | PowerBI | 12k  |
|    4 | Peter |   24 |    2 | PowerBI | 12k  |
+------+-------+------+------+---------+------+
```
## Нормализованный вид
Таблица курсов:
```sql
create table CourseDetails (cid int primary key, cname char(20) not null, fee char(10));
insert into CourseDetails values (1,'SQL','15k');
insert into CourseDetails values (2,'PowerBI','12k');
```
```
+------+---------+------+
| cid  | cname   | fee  |
+------+---------+------+
|    1 | SQL     | 15k  |
|    2 | PowerBI | 12k  |
+------+---------+------+
```

Таблица студентов
```sql
create table StudentDetails (
    sid int primary key, 
    name char(20) not null, 
    Age int check(Age>18), 
    Gender varchar(20) check (Gender='Male' or Gender='Female') ,
    cid int,
    foreign key(cid) references CourseDetails(cid)
);
insert into StudentDetails values (1, 'Ram', 21,'Male',1),(2,'Sana',23,'Female',1),(3,'John',27,'Male',2),(4,'Peter',24,'Male',2);
select * from StudentDetails;
```
```pseudographics
+-----+-------+------+--------+------+
| sid | name  | Age  | Gender | cid  |
+-----+-------+------+--------+------+
|   1 | Ram   |   21 | Male   |    1 |
|   2 | Sana  |   23 | Female |    1 |
|   3 | John  |   27 | Male   |    2 |
|   4 | Peter |   24 | Male   |    2 |
+-----+-------+------+--------+------+
```
# Преимущества
- уменьшает объем данных на диске
- увеличивает производительность
- ETL/Data Cleaning






