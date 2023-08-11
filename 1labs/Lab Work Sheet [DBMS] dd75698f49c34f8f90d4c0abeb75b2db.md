# Lab Work Sheet [DBMS]

```sql
C:\xampp\mysql\bin>mysql -h
localhost -u root
```

```sql
show databases;		/* Used to show the number of total databases */
```

```sql
show tables;		/* Used to show the number of tables in the selected database */
```

```sql
describe table_name;	/* Used to show the attributes of the tables */
```

## 1. Create Database “Bank” and display the list of databases.

```sql
create database bank;
show databases;
```

![Untitled](Lab%20Work%20Sheet%20%5BDBMS%5D%20dd75698f49c34f8f90d4c0abeb75b2db/Untitled.png)

![Untitled](Lab%20Work%20Sheet%20%5BDBMS%5D%20dd75698f49c34f8f90d4c0abeb75b2db/Untitled%201.png)

## 2. Drop the database “Bank” and display the list of databases.

```sql
drop database bank;
show databases;
```

![Untitled](Lab%20Work%20Sheet%20%5BDBMS%5D%20dd75698f49c34f8f90d4c0abeb75b2db/Untitled%202.png)

## 3. Create tables of given schema

```sql
use bank;
```

- **branch (branch_number, branch_city, assets)**

```sql
create table branch(
->branch_number int not null,
->branch_city varchar(20),
->assets varchar(25),
->constraint branch_num primary key(branch_number));
```

![Untitled](Lab%20Work%20Sheet%20%5BDBMS%5D%20dd75698f49c34f8f90d4c0abeb75b2db/Untitled%203.png)

![Untitled](Lab%20Work%20Sheet%20%5BDBMS%5D%20dd75698f49c34f8f90d4c0abeb75b2db/Untitled%204.png)

- **customer (customer_name, customer_street, customer_city)**

```sql
create table customer(
->customer_name varchar(20) not null PRIMARY KEY,
->customer_street varchar(45),
->customer_city varchar(25));
```

![Untitled](Lab%20Work%20Sheet%20%5BDBMS%5D%20dd75698f49c34f8f90d4c0abeb75b2db/Untitled%205.png)

- **loan (loan_number, branch_name, amount)**

```sql
create table loan(
->loan_number int not null,
->branch_number int not null,
->branch_name varchar(20),
->amount int,
->primary key(loan_number));
```

![Untitled](Lab%20Work%20Sheet%20%5BDBMS%5D%20dd75698f49c34f8f90d4c0abeb75b2db/Untitled%206.png)

- **borrower (customer_name, loan_number)**

```sql
create table borrower(
->customer_name varchar(25),
-> loan_number int,
->primary key(customer_name, loan_number),
->constraint fk_cus foreign key(customer_name) references
customer(customer_name),
->constraint fk_loan foreign key(loan_number) references
loan(loan_number));
```

![Untitled](Lab%20Work%20Sheet%20%5BDBMS%5D%20dd75698f49c34f8f90d4c0abeb75b2db/Untitled%207.png)

- **account (account_number, branch_name, balance)**

```sql
create table account(
->account_number int not null,
->branch_number int not null,
->branch_name varchar(20) not null,
->balance int,
->primary key(account_number),
->constraint fk_branch2 foreign key(branch_number) references
branch(branch_number));
```

![Untitled](Lab%20Work%20Sheet%20%5BDBMS%5D%20dd75698f49c34f8f90d4c0abeb75b2db/Untitled%208.png)

- **depositor (customer_name, account number)**

```sql
create table depositor(
->customer_name varchar(25),
->account_number int,
->primary key(customer_name, account_number),
->constraint fk_cus1 foreign key(customer_name) references
customer(customer_name),
->constraint fk_acc foreign key(account_number) references
account(account_number));
```

![Untitled](Lab%20Work%20Sheet%20%5BDBMS%5D%20dd75698f49c34f8f90d4c0abeb75b2db/Untitled%209.png)

## 4. List all the tables of Bank database

```sql
show tables;
```

![Untitled](Lab%20Work%20Sheet%20%5BDBMS%5D%20dd75698f49c34f8f90d4c0abeb75b2db/Untitled%2010.png)

## 5. List all the columns of “branch” and “customer” tables

```sql
describe branch;
describe customer;
```

![Untitled](Lab%20Work%20Sheet%20%5BDBMS%5D%20dd75698f49c34f8f90d4c0abeb75b2db/Untitled%2011.png)

## 6. Add column “Branch_manager” in branch table and list all the columns of branch table

```sql
alter table branch add branch_manager varchar(20);
```

![Untitled](Lab%20Work%20Sheet%20%5BDBMS%5D%20dd75698f49c34f8f90d4c0abeb75b2db/Untitled%2012.png)

## 7. Drop column “Branch_manager” from branch table and list all the columns of branch table

```sql
alter table branch drop branch_manager;
```

![Untitled](Lab%20Work%20Sheet%20%5BDBMS%5D%20dd75698f49c34f8f90d4c0abeb75b2db/Untitled%2013.png)

## 8. Change the data type of a column “balance” from decimal (12,2) to int in account table.

```sql
alter table account modify balance int;
```

![Untitled](Lab%20Work%20Sheet%20%5BDBMS%5D%20dd75698f49c34f8f90d4c0abeb75b2db/Untitled%2014.png)

## 9. Modify the length of data type “customer_name” from varchar (30)
to varchar (50) in a customer table.

```sql
alter table customer modify customer_name varchar(50);
```

![Untitled](Lab%20Work%20Sheet%20%5BDBMS%5D%20dd75698f49c34f8f90d4c0abeb75b2db/Untitled%2015.png)

## 10. Add a NOT NULL constraint in the column “branch_city” of the
branch table.

```sql
alter table branch modify column branch_city varchar(20) not null;
```

![Untitled](Lab%20Work%20Sheet%20%5BDBMS%5D%20dd75698f49c34f8f90d4c0abeb75b2db/Untitled%2016.png)

## 11. Add default constraint in “account” table and set default balance
is 1000. And list the columns of account table.

```sql
alter table account alter balance set default 10000;
describe account;
```

![Untitled](Lab%20Work%20Sheet%20%5BDBMS%5D%20dd75698f49c34f8f90d4c0abeb75b2db/Untitled%2017.png)

## 12. Drop the default constraint of balance from the account table and
list the columns of account table.

```sql
alter table account alter balance drop default;
```

![Untitled](Lab%20Work%20Sheet%20%5BDBMS%5D%20dd75698f49c34f8f90d4c0abeb75b2db/Untitled%2018.png)

## 13. Add Check constraint in “branch” Table assets must be greater than 100,00,000 and department city must be either KTM or PKR or BRT.

```sql
alter table branch(
->add constraint check_asset_city
->check (assets>10000000 and branch_city in ('KTM', 'PKR', 'BRT'));
```

![Untitled](Lab%20Work%20Sheet%20%5BDBMS%5D%20dd75698f49c34f8f90d4c0abeb75b2db/Untitled%2019.png)

## 14. Drop the check constraints from the branch table.

```sql
alter table branch drop constraint check_asset_city;
```

![Untitled](Lab%20Work%20Sheet%20%5BDBMS%5D%20dd75698f49c34f8f90d4c0abeb75b2db/Untitled%2020.png)

## 15. Add Primary Key constraint in table branch, customer, loan and
account based on relational schema. List the columns of all tables.

![Untitled](Lab%20Work%20Sheet%20%5BDBMS%5D%20dd75698f49c34f8f90d4c0abeb75b2db/Untitled%2021.png)

```sql
alter table account add primary key(account_number);
```

```sql
alter table borrower add primary key(customer_name, loan_number);
```

```sql
alter table branch add primary key(branch_number);
```

```sql
alter table customer add primary key(customer_name);
```

```sql
alter table depositor add primary key(customer_name, account_number);
```

```sql
alter table loan add primary key(loan_number);
Drop the primary key from the account table. List the columns of
account table.
```

```sql
alter table account drop primary key;
```

![Untitled](Lab%20Work%20Sheet%20%5BDBMS%5D%20dd75698f49c34f8f90d4c0abeb75b2db/Untitled%2022.png)

![Untitled](Lab%20Work%20Sheet%20%5BDBMS%5D%20dd75698f49c34f8f90d4c0abeb75b2db/Untitled%2023.png)

![Untitled](Lab%20Work%20Sheet%20%5BDBMS%5D%20dd75698f49c34f8f90d4c0abeb75b2db/Untitled%2024.png)

![Untitled](Lab%20Work%20Sheet%20%5BDBMS%5D%20dd75698f49c34f8f90d4c0abeb75b2db/Untitled%2025.png)

![Untitled](Lab%20Work%20Sheet%20%5BDBMS%5D%20dd75698f49c34f8f90d4c0abeb75b2db/Untitled%2026.png)

![Untitled](Lab%20Work%20Sheet%20%5BDBMS%5D%20dd75698f49c34f8f90d4c0abeb75b2db/Untitled%2027.png)

## 16. Add the foreign key constraints on the borrower and depositor table.

```sql
alter table borrower add constraint fk_const foreign key(customer_name)
->references customer(customer_name);
```

![Untitled](Lab%20Work%20Sheet%20%5BDBMS%5D%20dd75698f49c34f8f90d4c0abeb75b2db/Untitled%2028.png)

```sql
alter table borrower add constraint fk_const1 foreign key(loan_number)
->references loan(loan_number);
```

![Untitled](Lab%20Work%20Sheet%20%5BDBMS%5D%20dd75698f49c34f8f90d4c0abeb75b2db/Untitled%2029.png)

```sql
alter table depositor add constraint fk_const2 foreign key(customer_name)
->references customer(customer_name);
```

```sql
alter table depositor add constraint fk_const3 foreign key(account_number)
->references account(account_number);
```

![Untitled](Lab%20Work%20Sheet%20%5BDBMS%5D%20dd75698f49c34f8f90d4c0abeb75b2db/Untitled%2030.png)

## 17. Drop the foreign key constraints form depositor table.

```sql
alter table depositor drop constraint fk_const2;
```

```sql
alter table depositor drop constraint fk_const3;
```

![Untitled](Lab%20Work%20Sheet%20%5BDBMS%5D%20dd75698f49c34f8f90d4c0abeb75b2db/Untitled%2031.png)

## 18. Add unique constraints on “customer_name” column in the customer table.

```sql
alter table customer add constraint const2 unique(customer_name);
```

![Untitled](Lab%20Work%20Sheet%20%5BDBMS%5D%20dd75698f49c34f8f90d4c0abeb75b2db/Untitled%2032.png)

## 19. Drop the unique constraints from the customer table.

```sql
alter table customer drop index const2;
```

![Untitled](Lab%20Work%20Sheet%20%5BDBMS%5D%20dd75698f49c34f8f90d4c0abeb75b2db/Untitled%2033.png)

## 20. Add primary key constraint in the account table. And also add the foreign key constraints on the depositor table

```sql
alter table account add constraint pimarykey_acc primary key(account_number);
```

```sql
alter table depositor add constraint fkey_const1 foreign key(customer_name)
->references customer(customer_name);
```

```sql
alter
table depositor add constraint fkey_const2 foreign key(account_number)
->references account(account_number);
```

![Untitled](Lab%20Work%20Sheet%20%5BDBMS%5D%20dd75698f49c34f8f90d4c0abeb75b2db/Untitled%2034.png)