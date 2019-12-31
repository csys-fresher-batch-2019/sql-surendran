# office_database.md

*https://office_database.in

## features

* user should  be able to view employee details;

## features 1 to view the employees information
```sql
create table employee_details
(
    emp_id number(20) ,	         
    department_id number(20) not null,	
    employee_name varchar2(55) not null,
    birth_date date,
    joining_date date,
    constraint emp_dept_pk primary key(emp_id),
    constraint emp_fk foreign key (department_id) references departments(dept_id)
);

                      insert into EMPLOYEE_DETAILS (emp_id,employee_name,department_id,date_of_birth,joining_date,)
                      values (1,'anand',101,'21-APR-1990','10-DEC-2018'); 
                      
                      insert into EMPLOYEE_DETAILS (emp_id,employee_name,department_id,date_of_birth,joining_date)
                      values (2,'vijay',101,'22-MAY-1988','25-MAR-2015');
                      
                      insert into EMPLOYEE_DETAILS (emp_id,employee_name,department_id,date_of_birth,joining_date)
                      values (3,'ram',102,' 08-SEP-1996','10-DEC-2018');
                      
                      insert into EMPLOYEE_DETAILS (emp_id,employee_name,department_id,date_of_birth,joining_date)
                      values (4,'naveen',103,'06-SEP-1998','22-JUN-2017');
                     
                     select * from EMPLOYEE_DETAILS;
```
### features 2 to view the employees departments
``` sql
create table departments
( 
     dept_id number ,              --PRIMARY KEY
     department_name varchar2(20) not null,
     manager_id varchar2(20) not null,
     department_location varchar2(20),
     constraint dept_pk primary key(dept_id)
);

