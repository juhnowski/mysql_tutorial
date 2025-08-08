# Одна таблица
select колонки
    from имя таблицы
    where условия по фильтрации данных
    group by колонки для группировки
    having условия по фильтрации для агрегированных данных или вычисляемых полей
    order by поле для сортировки ASC|DESC 
    limit количество строк
# Много таблиц
    join
# Запросы
```sql
alter table StudentDetails add Location varchar(20);
```
+-----+-------+------+--------+------+----------+
| sid | name  | Age  | Gender | cid  | Location |
+-----+-------+------+--------+------+----------+
|   1 | Ram   |   21 | Male   |    1 | NULL     |
|   2 | Sana  |   23 | Female |    1 | NULL     |
|   3 | John  |   27 | Male   |    2 | NULL     |
|   4 | Peter |   24 | Male   |    2 | NULL     |
+-----+-------+------+--------+------+----------+

```sql
update StudentDetails set Location = 'NN' where sid in (1,3);
update StudentDetails set Location = 'Msk' where sid=2;
update StudentDetails set Location = 'SPb' where sid=4;
```

# DQL - Data Query Language
```sql
select * from StudentDetails;
select sid, name, Age, Gender, cid,  Location  from StudentDetails;
select *  from StudentDetails where Location = 'NN';
```
+-----+------+------+--------+------+----------+
| sid | name | Age  | Gender | cid  | Location |
+-----+------+------+--------+------+----------+
|   1 | Ram  |   21 | Male   |    1 | NN       |
|   3 | John |   27 | Male   |    2 | NN       |
+-----+------+------+--------+------+----------+

```sql
select count(*) as CountsOfStudents from StudentDetails;
```
+------------------+
| CountsOfStudents |
+------------------+
|                4 |
+------------------+

```sql
select count(*) as CountsOfStudents from StudentDetails where Location = 'NN';
```
 +------------------+
 | CountsOfStudents |
 +------------------+
 |                2 |
 +------------------+
```sql
select location,count(*) as CountsOfStudents from StudentDetails group by location;
```
+----------+------------------+
| location | CountsOfStudents |
+----------+------------------+
| NN       |                2 |
| Msk      |                1 |
| SPb      |                1 |
+----------+------------------+

```sql
select location,count(*) as CountsOfStudents from StudentDetails group by location having  CountsOfStudents > 1;
```
+----------+------------------+
| location | CountsOfStudents |
+----------+------------------+
| NN       |                2 |
+----------+------------------+

```sql
select * from StudentDetails order by name desc;
```
+-----+-------+------+--------+------+----------+
| sid | name  | Age  | Gender | cid  | Location |
+-----+-------+------+--------+------+----------+
|   2 | Sana  |   23 | Female |    1 | Msk      |
|   1 | Ram   |   21 | Male   |    1 | NN       |
|   4 | Peter |   24 | Male   |    2 | SPb      |
|   3 | John  |   27 | Male   |    2 | NN       |
+-----+-------+------+--------+------+----------+

```sql
select * from StudentDetails limit 1;
```
+-----+------+------+--------+------+----------+
| sid | name | Age  | Gender | cid  | Location |
+-----+------+------+--------+------+----------+
|   1 | Ram  |   21 | Male   |    1 | NN       |
+-----+------+------+--------+------+----------+

