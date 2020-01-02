# office_database.md

*https://office_database.in

## features

* user should  be able to view employee details;

## features 1 To view the employees information
```sql
create table employee_details
(
    emp_id number(20),
    employee_name varchar2(20) not null,	
    dept_id number(20) not null,
    joining_date date,            
    constraint emp_dept_pk primary key(emp_id),
    constraint emp_fk foreign key (dept_id) references departments(dept_id)
);

| emp_id | employee_name | dept_id       | joining_date | 
|--------|---------------|---------------|--------------|
| 1      | anand         | 1001           | 10-DEC-2018  |
| 2      | vijay         | 1001           | 25-MAR-2015  | 
| 3      | ram           | 1002           | 13-MAY-2016  | 
  
```
### features 2 To view the  departments 
``` sql
create table departments
( 
     dept_id number ,              --PRIMARY KEY
     dept_name varchar2(20) not null,
     constraint dept_pk primary key(dept_id)
);


| dept_id | dept_name       | 
|---------|-----------------|
| 1001    | HR              |      
| 1002    | sales           | 
| 1003    | development     |  

```
#### features 3 To view the salary details

```sql
create table salary(
emp_id number not null,
base_pay number not null,
allowance number,
salary_increment number,
total_salary number,
constraint emp_id_fk foreign key(emp_id) references employee_details(emp_id),
constraint salary_ck check (total_salary >= 0));


| emp_id | base_pay | allowance | salary_increment | total_salary |
|--------|----------|-----------|------------------|--------------|
| 1      | 8000     | 1000      | 0                | 0            |
| 2      | 13000    | 1500      | 0                | 0            |
| 3      | 9500     | 500       | 0                | 0            |


```
