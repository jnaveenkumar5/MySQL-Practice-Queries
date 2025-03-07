# MySQL-Practice-Queries
## Creating database
```
create database sql_intro;
show databases;
use sql_intro;
```
## Creating Table
```
create table emp_details(Name varchar(20),Age int,Sex char(1),
doj date,City varchar(20),Salary float);
describe emp_details;
show databases;
use sql_intro;
```
## inserting Table values
```
insert into emp_details
values("kumar",23,"M","2002-08-05",20000),
       ("Nikil",35,"M","2022-08-13","skl",15000),
       ("sailaja","30","F","2006-02-05",25000);
select distinct city from emp_details;
select avg(salary) from emp_details;
select * from emp_details;
select (10+20) as addition;
select length("India");
select repeat('@',20);
select lower('kUMARABAar');
select curdate();
select year('2025-1-14')
select concat('hello','    ','world')
```
## Time and date Formates
```
select day(current_date());
select year(now());
select ifnull(23,'default value') as result;
select date_format('2025-1-1','%Y');
select week('2025-06-15') as weekNumber;
select date_format('2025-06-15 14:30:45','%H%h%i%s%p%r%T');
select time(now());
select current_time();
select current_timestamp();
select date_format(now(),'%W-%M%d-%y');
alter table emp_details add email varchar(50);
select * from emp_details where salary like '15000';
```
## primary key ,check,unique,notnull
```
create table customer(emp_id int primary key, Name varchar(50) not null, email varchar(100) unique ,
salary decimal(10,2), price decimal(10,2) check (price>0));
desc employees;
select * from customer;
insert customer values(1,'fhhks','gmailhksjfk@gmail.com',2500,300);
 insert customer values(5,'kumar','isjfk@gmail.com',2500,677);
```
 ## sql joins
 ```
 create table cricket(cricket_id int auto_increment,name varchar(30),primary key(cricket_id));
 
  create table football(football_id int auto_increment,name varchar(30),primary key(football_id));
insert into cricket (name)
values ('Kumar'),('Ashok'),('babu'),('Koti'),('Naveen');
select * from cricket;
insert into football (name)
values ('Kumar'),('Koti'),('Ashok'),('Lokesh'),('Likith');
select * from football;
SELECT * from cricket as c inner join
football as f on c.name=f.name;
select c.cricket_id,c.name,f.football_id,f.name from
cricket as c right join football as f using(name);  
```
## DDL commands
use sql_intro;
show tables;
-- create command
create table employees(
  empid int auto_increment primary key,
  firstname varchar(10) not null,
  lastname varchar(10) not null,
  hiredate date,
  salary decimal(10,2)
  );
  -- alter command 
  -- adding column
  alter table employees add email varchar(100);
  select * from employees;
  -- modifying column
  alter table employees modify salary decimal(12,3);
  -- drop column
  alter table employees drop email;
  -- drop command and truncate command truncate table table_name
  -- rename command
  rename table employees to staff;
    select * from staff;
```
## DML commands
```
-- insert command
insert into staff
values(null,'naveen','kumar','2020-1-5',25000,'hjdgmail.com');
select current_date();
select curdate();
select current_timestamp();
select current_user();
select curtime();
desc staff;
select * from staff;
  -- update
  update staff set salary=15000
  where empid=1;
  -- Delete
  delete from staff where empid=1;
  select * from emp;
```
## Window Functions
```
  select row_number() over (partition by job order by sal desc) as rownumder,ename,sal,job,deptno,mgr from emp;
select first_value(job) over (partition by job order by sal asc) as highestpaid,ename,sal,job,deptno,mgr from emp;
  select lag(sal) over (order by sal desc) as Next_salary,ename,sal,job,deptno,mgr from emp;
    select sal,dense_rank() over (order by sal desc) as Rank_num from emp limit 1 offset 2;
   select dense_rank() over (order by sal desc) as dense_rank_num,sal,job,deptno,mgr from emp;
    select * from emp where sal=(select max(sal) from emp);
    select max(sal) as second_highest_salary from emp where sal < (select max(sal) from emp);
    use sql_intro;
create table dept(   
  deptno     int(20),   
  dname      varchar(14),   
  loc        varchar(13),   
  constraint pk_dept primary key (deptno)   
);
insert into dept
values(10, 'ACCOUNTING', 'NEW YORK');
insert into dept
values(20, 'RESEARCH', 'DALLAS');
insert into dept
values(30, 'SALES', 'CHICAGO');
insert into dept
values(40, 'OPERATIONS', 'BOSTON');
select * from dept;
create table emp(   
  empno    int(4),   
  ename    varchar(10),   
  job      varchar(9),   
  mgr      int(4),   
  hiredate date,   
  sal      float(7,2),   
  comm     int(7),   
  deptno   int(2),   
  constraint pk_emp primary key (empno),   
  constraint fk_deptno foreign key (deptno) references dept (deptno)   
);
INSERT INTO emp
VALUES
(7839, 'KING', 'PRESIDENT', NULL, 
 '1981-11-17', 5000, NULL, 10);

INSERT INTO emp
VALUES
(7698, 'BLAKE', 'MANAGER', 7839, 
 '1981-05-01', 2850, NULL, 30);

INSERT INTO emp
VALUES
(7782, 'CLARK', 'MANAGER', 7839, 
 '1981-06-09', 2450, NULL, 10);

INSERT INTO emp
VALUES
(7566, 'JONES', 'MANAGER', 7839, 
 '1981-04-02', 2975, NULL, 20);

INSERT INTO emp
VALUES
(7788, 'SCOTT', 'ANALYST', 7566, 
 DATE_ADD('1987-07-13', INTERVAL -85 DAY), 3000, NULL, 20);

INSERT INTO emp
VALUES
(7902, 'FORD', 'ANALYST', 7566, 
 '1981-12-03', 3000, NULL, 20);

INSERT INTO emp
VALUES
(7369, 'SMITH', 'CLERK', 7902, 
 '1980-12-17', 800, NULL, 20);

INSERT INTO emp
VALUES
(7499, 'ALLEN', 'SALESMAN', 7698, 
 '1981-02-20', 1600, 300, 30);

INSERT INTO emp
VALUES
(7521, 'WARD', 'SALESMAN', 7698, 
 '1981-02-22', 1250, 500, 30);

INSERT INTO emp
VALUES
(7654, 'MARTIN', 'SALESMAN', 7698, 
 '1981-09-28', 1250, 1400, 30);

INSERT INTO emp
VALUES
(7844, 'TURNER', 'SALESMAN', 7698, 
 '1981-09-08', 1500, 0, 30);

INSERT INTO emp
VALUES
(7876, 'ADAMS', 'CLERK', 7788, 
 DATE_ADD('1987-07-13', INTERVAL -51 DAY), 1100, NULL, 20);

INSERT INTO emp
VALUES
(7900, 'JAMES', 'CLERK', 7698, 
 '1981-12-03', 950, NULL, 30);

INSERT INTO emp
VALUES
(7934, 'MILLER', 'CLERK', 7782, 
 '1982-01-23', 1300, NULL, 10);
 select * from emp where deptno=10;
 select * from emp as e  left join dept as d on e.deptno=d.deptno;
 select * from dept;
 select * from emp;
 select ename,job,sum(sal) as total_salary from emp group by ename,job with rollup;
 select * from emp order by sal desc limit 1;
```
## Agregate functions
```
SELECT * FROM sql_intro.emp;
# agregate functions
select job,
count(*) as total_empnumbers,
avg(sal) as average_salary,
sum(sal) as total_salary,
max(sal) as maximum_sal,
min(sal) as mini_sal from emp group by job;
```
## case statement
```
select ename,sal,
case 
    when sal<1000 then 'Low'
    when sal between 1000 and 3000 then 'Medium'
    else 'High'
end as salary_category
from emp;
```
## if statement
```
select ename,sal,
if(sal>3000 ,'Eligible','Not Eligible') as bonus_status
from emp;
```
## ifnull 
```
select ename,sal,comm,ifnull(comm,0) as comm_zero from emp;
```   

    
