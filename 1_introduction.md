# Подготовка
sudo systemctl start mysql
sudo systemctl enable mysql
sudo systemctl status mysql
mysql --version
mysql  Ver 8.0.42-0ubuntu0.24.04.2 for Linux on x86_64 ((Ubuntu))

sudo mysql -h localhost

CREATE USER 'ilya'@'localhost' IDENTIFIED BY '1';
```sql
show databases;
create database sql_practice;
use sql_practice;
create table StudentTable(StudentId int, Name char(20), Age int, Gender char(10));
show tables;
insert into StudentTable values(1,'Ilya',47,'Male');
insert into StudentTable values(2,'John',48,'Male'),(3,'Nataliya',48,'Female');
select * from StudentTable;
drop table StudentTable;
```


