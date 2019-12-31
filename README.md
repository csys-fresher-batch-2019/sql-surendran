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
    pan_card varchar2(20) NOT NULL,     
    adhar_num  number(15),             
    constraint emp_dept_pk primary key(emp_id),
    constraint emp_adhar unique(adhar_num),
    constraint emp_fk foreign key (department_id) references departments(dept_id)
);

                      insert into EMPLOYEE_DETAILS (emp_id,employee_name,department_id,date_of_birth,joining_date,pan_card,adhar_num)
                      values (1,'anand',101,'21-APR-1990','10-DEC-2018','cfs123568dd','546390'); 
                      
                      insert into EMPLOYEE_DETAILS (emp_id,employee_name,department_id,date_of_birth,joining_date,pan_card,adhar_num)
                      values (2,'vijay',101,'22-MAY-1988','25-MAR-2015','asc212789ds','549389');
                      
                      insert into EMPLOYEE_DETAILS (emp_id,employee_name,department_id,date_of_birth,joining_date,pan_card,adhar_num)
                      values (3,'ram',102,' 08-SEP-1996','10-DEC-2018','bsc1789398j','548927');
                      
                      insert into EMPLOYEE_DETAILS (emp_id,employee_name,department_id,date_of_birth,joining_date,pan_card,adhar_num)
                      values (4,'naveen',103,'06-SEP-1998','22-JUN-2017','kxh837728hh','572922');
                     
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

