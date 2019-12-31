# office_database.md

*https://office_database.in

## features

* user should  be able to view employee details;

## features to view the employees information
```sql
create table employee_details
(
    emp_id number(20) ,	         
    department_id number(20) not null,	
    employee_name varchar2(55) not null,
    birth_date date,
    joining_date date,
    pan_card varchar2(20) NOT NULL,     
    adhar_num  number(15),             
    constraint emp_dept_pk primary key(emp_id),
    constraint emp_adhar unique(adhar_num),
    constraint emp_fk foreign key (department_id) references departments(dept_id)
);
```
