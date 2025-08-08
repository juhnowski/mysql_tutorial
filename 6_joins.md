# Мощность / Отношения
- 1-1 страна - президент
- 1-* отдел - сотрудники
- *-* курс - студент

# Inner Join - совпадающие значения (MV - matching values)
```sql
use StudentDB;
select * from StudentDetails as SD 
	join CourseDetails as CD
	on SD.cId = CD.cId;
```
```
+-----+-------+------+--------+------+----------+-----+---------+------+
| sid | name  | Age  | Gender | cid  | Location | cid | cname   | fee  |
+-----+-------+------+--------+------+----------+-----+---------+------+
|   1 | Ram   |   21 | Male   |    1 | NN       |   1 | SQL     | 15k  |
|   2 | Sana  |   23 | Female |    1 | Msk      |   1 | SQL     | 15k  |
|   3 | John  |   27 | Male   |    2 | NN       |   2 | PowerBI | 12k  |
|   4 | Peter |   24 | Male   |    2 | SPb      |   2 | PowerBI | 12k  |
+-----+-------+------+--------+------+----------+-----+---------+------+
```

# Outer Joins
- left join = MV + UML
- right join = MV + UMR
- full join = MV + UMBoth


```sql
insert into CourseDetails values (3,'Python','10k');
select * from CourseDetails;
```
```
+-----+---------+------+
| cid | cname   | fee  |
+-----+---------+------+
|   1 | SQL     | 15k  |
|   2 | PowerBI | 12k  |
|   3 | Python  | 10k  |
+-----+---------+------+
```
```sql
insert into StudentDetails values(5,'Ilya',30,'Male',null,'NN');
```
```
+-----+-------+------+--------+------+----------+
| sid | name  | Age  | Gender | cid  | Location |
+-----+-------+------+--------+------+----------+
|   1 | Ram   |   21 | Male   |    1 | NN       |
|   2 | Sana  |   23 | Female |    1 | Msk      |
|   3 | John  |   27 | Male   |    2 | NN       |
|   4 | Peter |   24 | Male   |    2 | SPb      |
|   5 | Ilya  |   30 | Male   | NULL | NN       |
+-----+-------+------+--------+------+----------+
```
## Left Join
```sql
select * from StudentDetails as SD
	left join CourseDetails as CD
	on SD.cId = CD.cId;
```
```
+-----+-------+------+--------+------+----------+------+---------+------+
| sid | name  | Age  | Gender | cid  | Location | cid  | cname   | fee  |
+-----+-------+------+--------+------+----------+------+---------+------+
|   1 | Ram   |   21 | Male   |    1 | NN       |    1 | SQL     | 15k  |
|   2 | Sana  |   23 | Female |    1 | Msk      |    1 | SQL     | 15k  |
|   3 | John  |   27 | Male   |    2 | NN       |    2 | PowerBI | 12k  |
|   4 | Peter |   24 | Male   |    2 | SPb      |    2 | PowerBI | 12k  |
|   5 | Ilya  |   30 | Male   | NULL | NN       | NULL | NULL    | NULL |
+-----+-------+------+--------+------+----------+------+---------+------+
```
## Right Join
```sql
select * from StudentDetails as SD
	right join CourseDetails as CD
	on SD.cId = CD.cId;
``` 
```
+------+-------+------+--------+------+----------+-----+---------+------+
| sid  | name  | Age  | Gender | cid  | Location | cid | cname   | fee  |
+------+-------+------+--------+------+----------+-----+---------+------+
|    2 | Sana  |   23 | Female |    1 | Msk      |   1 | SQL     | 15k  |
|    1 | Ram   |   21 | Male   |    1 | NN       |   1 | SQL     | 15k  |
|    4 | Peter |   24 | Male   |    2 | SPb      |   2 | PowerBI | 12k  |
|    3 | John  |   27 | Male   |    2 | NN       |   2 | PowerBI | 12k  |
| NULL | NULL  | NULL | NULL   | NULL | NULL     |   3 | Python  | 10k  |
+------+-------+------+--------+------+----------+-----+---------+------+
```
## Full Join
###  Implicit CROSS JOIN
```sql
select * from StudentDetails,CourseDetails;
```
### Cross Join

select * from StudentDetails
	cross join CourseDetails;
```
+-----+-------+------+--------+------+----------+-----+---------+------+
| sid | name  | Age  | Gender | cid  | Location | cid | cname   | fee  |
+-----+-------+------+--------+------+----------+-----+---------+------+
|   1 | Ram   |   21 | Male   |    1 | NN       |   3 | Python  | 10k  |
|   1 | Ram   |   21 | Male   |    1 | NN       |   2 | PowerBI | 12k  |
|   1 | Ram   |   21 | Male   |    1 | NN       |   1 | SQL     | 15k  |
|   2 | Sana  |   23 | Female |    1 | Msk      |   3 | Python  | 10k  |
|   2 | Sana  |   23 | Female |    1 | Msk      |   2 | PowerBI | 12k  |
|   2 | Sana  |   23 | Female |    1 | Msk      |   1 | SQL     | 15k  |
|   3 | John  |   27 | Male   |    2 | NN       |   3 | Python  | 10k  |
|   3 | John  |   27 | Male   |    2 | NN       |   2 | PowerBI | 12k  |
|   3 | John  |   27 | Male   |    2 | NN       |   1 | SQL     | 15k  |
|   4 | Peter |   24 | Male   |    2 | SPb      |   3 | Python  | 10k  |
|   4 | Peter |   24 | Male   |    2 | SPb      |   2 | PowerBI | 12k  |
|   4 | Peter |   24 | Male   |    2 | SPb      |   1 | SQL     | 15k  |
|   5 | Ilya  |   30 | Male   | NULL | NN       |   3 | Python  | 10k  |
|   5 | Ilya  |   30 | Male   | NULL | NN       |   2 | PowerBI | 12k  |
|   5 | Ilya  |   30 | Male   | NULL | NN       |   1 | SQL     | 15k  |
+-----+-------+------+--------+------+----------+-----+---------+------+
```
всего 5*3=15 записей

### Self join - join таблицы на саму себя
```sql
CREATE TABLE Employees (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(100),
    manager_id INT
);

INSERT INTO Employees (employee_id, employee_name, manager_id) VALUES
(1, 'John Smith', NULL),
(2, 'Mary Johnson', 1),
(3, 'Sam Brown', 1),
(4, 'Alice White', 2);

SELECT
    e.employee_name AS Employee,
    m.employee_name AS Manager
FROM
    Employees AS e
LEFT JOIN
    Employees AS m ON e.manager_id = m.employee_id;
```




