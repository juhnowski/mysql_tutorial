```sql
create database BesantBank;

use  BesantBank;

create table  BesantBank;(
     TransactionDetails(int primary key,
    Name char(30) not null,
    Age tinyint check(age>18),
    AccountType varchar(20),
    CurrentBalance int
);

insert into AccountId ccountDetails values(1,'Ilya',21,'Saving',1000);
 
select * from AccountDetails; 

create table TransactionDetails(
    TransactionId int primary key auto_increment,
    AccountId int,
    TransactionType varchar(10) check(TransactionType='Credit' or TransactionType='Debit'),
    TransactionAmount int,
    TransactionTime datetime default(now()),
    foreign key (AccountId) references AccountDetails(AccountId)  
);

insert into TransactionDetails (AccountId, TransactionType, TransactionAmount) values (1,'Credit',1000);   
insert into TransactionDetails (AccountId, TransactionType, TransactionAmount) values (1,'Debit',500); 

select * from  TransactionDetails;  
```
