Exp 4
Departments Table
CREATE TABLE departments (
    deptno INT PRIMARY KEY,
    dept_name VARCHAR(50),
    location VARCHAR(50)
);

INSERT INTO departments (deptno, dept_name, location) VALUES (10, 'ACCOUNTING', 'New York');
INSERT INTO departments (deptno, dept_name, location) VALUES (20, 'RESEARCH', 'Dallas');
INSERT INTO departments (deptno, dept_name, location) VALUES (30, 'SALES', 'Chicago');
INSERT INTO departments (deptno, dept_name, location) VALUES (40, 'OPERATIONS', 'Boston');


Employee Table
CREATE TABLE emp6 (
    emp_no INT PRIMARY KEY,
    birth_date DATE NOT NULL,
    first_name VARCHAR(14) NOT NULL,
    last_name VARCHAR(16) NOT NULL,
    gender varchar2(1)check (gender in ('M','F')) NOT NULL,
    hire_date DATE NOT NULL,
    salary FLOAT DEFAULT 7850.00,
    job VARCHAR(20) NOT NULL,
    deptno INT,
    manager_id INT,
    FOREIGN KEY (deptno) REFERENCES departments(deptno)
);
INSERT INTO emp6 (emp_no, birth_date, first_name, last_name, gender, hire_date, salary, job, deptno, manager_id) VALUES (7839, date'1955-11-17', 'John', 'Smith', 'M', date'1990-06-09', 5000.00, 'MANAGER', 10, NULL);
INSERT INTO emp6 (emp_no, birth_date, first_name, last_name, gender, hire_date, salary, job, deptno, manager_id) VALUES (7566, date'1960-02-21', 'James', 'Brown', 'M',date '1991-04-02', 2450.00, 'CLERK', 20, 7839);
INSERT INTO emp6 (emp_no, birth_date, first_name, last_name, gender, hire_date, salary, job, deptno, manager_id) VALUES (7654, date'1963-12-09', 'Scott', 'Allen', 'M', date'1989-06-04', 2975.00, 'SALESMAN', 30, 7839);
INSERT INTO emp6 (emp_no, birth_date, first_name, last_name, gender, hire_date, salary, job, deptno, manager_id) VALUES (7934, date'1970-12-03', 'Adam', 'Martin', 'M', date'1993-07-09', 1300.00, 'CLERK', 30, 7839);
INSERT INTO emp6 (emp_no, birth_date, first_name, last_name, gender, hire_date, salary, job, deptno, manager_id) VALUES (7788, date'1961-05-23', 'Alan', 'Walker', 'M', date'1990-09-14', 3000.00, 'ANALYST', 20, 7566);
INSERT INTO emp6 (emp_no, birth_date, first_name, last_name, gender, hire_date, salary, job, deptno, manager_id) VALUES (7902, date'1958-11-07', 'Alice', 'Jones', 'F', date'1988-12-12', 1600.00, 'CLERK', 30, 7654);
INSERT INTO emp6 (emp_no, birth_date, first_name, last_name, gender, hire_date, salary, job, deptno, manager_id) VALUES (7876, date'1962-01-14', 'George', 'Black', 'M', date'1989-01-20', 1100.00, 'CLERK', 40, 7566);
INSERT INTO emp6 (emp_no, birth_date, first_name, last_name, gender, hire_date, salary, job, deptno, manager_id) VALUES (7844, date'1965-09-28', 'Diana', 'White', 'F', date'1992-05-21', 2950.00, 'SALESMAN', 30, 7654);
INSERT INTO emp6 (emp_no, birth_date, first_name, last_name, gender, hire_date, salary, job, deptno, manager_id) VALUES (7900, date'1972-06-19', 'Bob', 'King', 'M', date'1991-08-18', 850.00, 'CLERK', 10, 7839);
--------------------------------------------------------------------------------------------
1.Display all employee names that starts with "a" and are at least 3 characters in length.
==>select first_name,last_name from emp6 where lower(first_name)like 'a%' and length(first_name)>=3;
greater than 4
==>select first_name,last_name from emp6 where lower(first_name)like 'a%' and length(first_name)>4;
2.Display departments having Dollas, New York and Chicago locations.
==>select*from departments;
select*from departments where lower(location)='dallas' or lower(location)='new york' or lower(location)='chicago';
3.Display the names of employees who are working as clerk, salesman or analyst and drawing a salary more than 3000.
==>select first_name,job,salary from emp6 where lower(job) IN('clerk','salesman','analyst') and salary >= 3000;
select first_name,job,salary from emp6; #to check
4.Display the names of employees who are not working as managers.
==>select first_name from emp6 where job != 'MANAGER';
5.Display the name of emp who earns highest salary.
==>select first_name,salary from emp6 where salary=(select max(salary)from emp6);
6.Display the employee number and name of employee working as CLERK and earning highest salary among CLERKS.
==>select emp_no,first_name,salary from emp6 where salary=(select max(salary)from emp6 where lower(job)='clerk');
7.Display the names of clerks who earn salary more than that of James of that of sal lesser  than that of Bob.
==>select first_name from emp6 where job='CLERK' and salary <(select salary from emp6 where first_name='James')and salary>(select salary from emp6 where first_name='Bob'); 
or 
select emp_no,first_name,salary from emp6 where lower(job)='clerk' and salary>(select salary from emp6 where lower(first_name)='bob')and salary<(select salary from emp6 where lower (first_name)='james');
8.Display the names of the employees who earn highest salary in their respective departments.
==>select e.first_name,e.salary,e.deptno from emp6 e where e.salary=(select max(salary)from emp6 where deptno=e.deptno);
