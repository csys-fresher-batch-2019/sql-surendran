# office_database.md

*https://office_database.in

## features

* user should  be able to view employee details;

## features 1 To view the employees information
```sql
create table employee_details
(
    emp_id number(20) ,	         	
    employee_name varchar2(55) not null,
     dept_id number(20) not null,
    joining_date date,
    sex char(1) check (sex in('m','f')),
    constraint emp_dept_pk primary key(emp_id),
    constraint emp_fk foreign key (department_id) references departments(dept_id)
);

      CREATE SEQUENCE emp_ID_SEQ START WITH 1 INCREMENT BY 1;

      insert into EMPLOYEE_DETAILS (emp_id,employee_name,dept_id,joining_date)
      values (emp_ID_SEQ.nextval,'vijay',101,'25-MAR-2015');
      insert into EMPLOYEE_DETAILS (emp_id,employee_name,dept_id,joining_date,sex)
      values (emp_ID_SEQ.nextval,'vijay',101,'25-MAR-2015','m');
      insert into EMPLOYEE_DETAILS (emp_id,employee_name,dept_id,joining_date,sex)
      values (emp_ID_SEQ.nextval,'isha',102,' 13-MAY-2016','f');

| emp_id  |  employee_name  |  dept_id | joining_date | sex |
|---------|-----------------|----------|--------------|-----|
| 1       | anand           | 101      | 10-DEC-2018  | m   |
| 2       | vijay           | 101      | 25-MAR-2015  | m   |
| 3       | isha            | 102      | 13-MAY-2016  | f   |
```
### features 2 To view the  departments 
``` sql
create table departments
( 
     dept_id number ,              --PRIMARY KEY
     dept_name varchar2(20) not null,
     constraint dept_pk primary key(dept_id)
);



insert into departments( dept_id,department_name)
values (101,'hr');

insert into departments( dept_id,department_name)
values (102,'dba');

insert into departments( dept_id,department_name)
values (103,'sales');



| dept_id | dept_name       | 
|---------|-----------------|
| 101     | HR              |      
| 102     | dba             | 
| 103     | sales           |  

```
#### features 3 To view the salary details
``` sql
create table salary(
emp_id number not null,
base_pay number not null,
allowance number,
salary_increment number,
total_salary number,
constraint emp_id_fk foreign key(emp_id) references employee_details(emp_id),
constraint salary_ck check (total_salary >= 0));

insert into salary(emp_id,base_pay,allowance,salary_increment,total_salary)
            values(1,10000,500,0,10500);
insert into salary(emp_id,base_pay,allowance,salary_increment,total_salary)
            values(2,12500,500,1000,14000);
insert into salary(emp_id,base_pay,allowance,salary_increment)
            values(3,14500,500,2000,15000);


| emp_id | base_pay  | allowance | salary_increment | total_salary |
|--------|---------- |-----------|------------------|--------------|
| 1      | 10000     | 500       | 0                | 10500        |
| 2      | 12500     | 500       | 1000             | 14000        |
| 3      | 14500     | 500       | 2000             | 15000        |
```

##### secnario
```
*   select e.dept_id,e.emp_id,e.employee_name,d.department_name,s.total_salary from EMPLOYEE_DETAILS e,departments d,salary s 
   where e.dept_id = d.dept_id and s.emp_id =e.emp_id
   
| 101 | 1 | anand   | HR    | 11000 |
|-----|---|---------|-------|-------|
| 101 | 2 | vijay   | HR    | 15500 |
| 102 | 3 | isha    | DBA   | 15000 |
| 103 | 4 | suriya  | sales | 17500 |
| 102 | 5 | punitha | DBA   | 13000 |
 
   
*   select employee_name, floor((sysdate-joining_date)/365)as Experience from employee_details 
| anand   | 1 |
|---------|---|
| vijay   | 4 |
| isha    | 3 |
| suriya  | 6 |
| punitha | 9 |


update salary set salary_increment =2000 where emp_id=3

| 1 | 10000 | 1000 | 0    | 11000 |
|---|-------|------|------|-------|
| 2 | 12500 | 2000 | 1000 | 15500 |
| 3 | 14500 | 500  | 2000 | 15000 |
| 4 | 15000 | 500  | 2000 | 17500 |
| 5 | 11000 | 500  | 1500 | 13000 |

*   update salary set allowance=2000 where emp_id=3


| 1 | 10000 | 1000 | 0    | 11000 |
|---|-------|------|------|-------|
| 2 | 12500 | 2000 | 1000 | 15500 |
| 3 | 14500 | 2000 | 2000 | 16500 |
| 4 | 15000 | 500  | 2000 | 17500 |
| 5 | 11000 | 500  | 1500 | 13000 |

create or replace PROCEDURE TOTAL_SALARY 
(
   eid IN NUMBER 
) 
AS 
BEGIN

update salary set total_salary=total_salary+salary_increment where emp_id=eid;
update salary set total_salary=allowance
+base_pay where emp_id=eid;
END TOTAL_SALARY;


to run PROCEDURE

exec total_salary(3);

| 1 | 10000 | 1000 | 0    | 11000 |
|---|-------|------|------|-------|
| 2 | 12500 | 2000 | 1000 | 15500 |
| 3 | 14500 | 2000 | 2000 | 18500 |
| 4 | 15000 | 500  | 2000 | 17500 |
| 5 | 11000 | 500  | 1500 | 13000 |


* select e.dept_id,e.emp_id,e.employee_name,d.department_name,s.total_salary from EMPLOYEE_DETAILS e,departments d,salary s 
where e.dept_id = d.dept_id and s.emp_id =e.emp_id and s.total_salary >15000

| 101 | 2 | vijay  | HR    | 15500 |
|-----|---|--------|-------|-------|
| 102 | 3 | isha   | DBA   | 18500 |
| 103 | 4 | suriya | sales | 17500 |
