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

| emp_id  |  employee_name  |  dept_id | joining_date | sex |
|---------|-----------------|----------|--------------|-----|
| 1       | anand           | 101      | 10-DEC-2018  | m   |
| 2       | vijay           | 101      | 25-MAR-2015  | m   |
| 3       | isha            | 102      | 13-MAY-2016  | f   |

      insert into EMPLOYEE_DETAILS (emp_id,employee_name,dept_id,joining_date)
      values (emp_ID_SEQ.nextval,'vijay',101,'25-MAR-2015');
      insert into EMPLOYEE_DETAILS (emp_id,employee_name,dept_id,joining_date,sex)
      values (emp_ID_SEQ.nextval,'vijay',101,'25-MAR-2015','m');
      insert into EMPLOYEE_DETAILS (emp_id,employee_name,dept_id,joining_date,sex)
      values (emp_ID_SEQ.nextval,'isha',102,' 13-MAY-2016','f');


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
| 101     | HR              |      
| 102     | dba             | 
| 103     | sales           |  


insert into departments( dept_id,department_name)
values (101,'hr');

insert into departments( dept_id,department_name)
values (102,'dba');

insert into departments( dept_id,department_name)
values (103,'sales');
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


| emp_id | base_pay  | allowance | salary_increment | total_salary |
|--------|---------- |-----------|------------------|--------------|
| 1      | 10000     | 500       | 0                | 10500        |
| 2      | 12500     | 500       | 1000             | 14000        |
| 3      | 14500     | 500       | 2000             | 15000        |


insert into salary(emp_id,base_pay,allowance,salary_increment,total_salary)
            values(1,10000,500,0,10500);
insert into salary(emp_id,base_pay,allowance,salary_increment,total_salary)
            values(2,12500,500,1000,14000);
insert into salary(emp_id,base_pay,allowance,salary_increment)
            values(3,14500,500,2000,15000);

```
