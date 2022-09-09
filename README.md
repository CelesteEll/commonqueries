# top basic sql queries

CREATE DATABASE IF NOT EXISTS final_practise; 
-- To drop the databse--
-- DROP DATABASE IF EXISTS final_practise; -- 


CREATE TABLE IF NOT EXISTS Employee (
employee_id INT  PRIMARY KEY AUTO_INCREMENT,
first_name VARCHAR(255) NOT NULL,
last_name VARCHAR(255) NOT NULL,
gender CHAR(1) NOT NULL,
position VARCHAR(255) NOT NULL,
department_id INT NOT NULL,
salary INT NOT NULL,
FOREIGN KEY (department_id) REFERENCES department(department_id) 
);

CREATE TABLE IF NOT EXISTS department 
(
 department_id INT PRIMARY KEY,
 department_name VARCHAR(255) NOT NULL ) ; 
 
 INSERT INTO Employee VALUES (2002, 'Super', 'Man', 'M', 'Tester', 1, 75000);
 INSERT INTO Employee VALUES (DEFAULT, 'Jessica', 'lyers', 'F', 'Architect', 1, 60000) ; 
 insert into employee values (2004, "Bonnie", "Adams", "F", "Project Manager", 1, 80000);
insert into employee values (2005, "James", "Madison", "M", "Software Developer", 1, 55000);
insert into employee values (2006, "Michael", "Greenback", "M", "Sales Assistant", 2, 85000);
insert into employee values (2007, "Leslie", "Peters", "F", "Sales Engineer", 2, 76000);
insert into employee values (2008, "Max", "Powers", "M", "Sales Representative", 2, 59000);
insert into employee values (2009, "Stacy", "Jacobs", "F", "Sales Manager", 2, 730000);
insert into employee values (2010, "John", "Henery", "M", "Sales Director", 2, 90000);

INSERT INTO department VALUES ( 1, 'IT'),
							  (2, 'Sales') ; 
                              

                 -- QUESTIONS--

-- return employee record with max salary (meaning get all info about employee with max salary)
SELECT *
FROM employee
WHERE salary =
(SELECT MAX(salary)
FROM employee) ;


-- select highest salary from the employee table
SELECT MAX(salary)
FROM employee;

-- select second highest slary in employee table
SELECT *
FROM employee
ORDER BY SALARY DESC
LIMIT 1,1; 

-- select range of employee based on id
SELECT *
FROM employee
WHERE employee_id BETWEEN 2004 AND 2009; 

-- Return employee name, highest salary and department

SELECT
  employee_id,
  CONCAT(first_name, '', last_name) AS name ,
  MAX(salary),
  department_name
FROM employee e
JOIN department d
USING(department_id)
GROUP BY  employee_id,
     name,
    department_name
ORDER BY MAX(salary) DESC; 


-- Return highest salary, employee name, department name for each department
SELECT 
 salary,
 first_name,
 department_name 
FROM employee e
JOIN department d
USING(department_id)
WHERE salary IN (
SELECT MAX(salary)
FROM employee
GROUP BY department_id ) ; 


-- Return the third highest salary from employee
SELECT salary
FROM employee
ORDER BY salary DESC
LIMIT 2,1; 

-- Find SQL query to find duplicate rows in the table

SELECT *, COUNT(employee_id)
FROM employee
GROUP BY employee_id 
HAVING COUNT(employee_id) > 1 ;

-- Return the first and last record from the table

SELECT *
FROM employee
WHERE employee_id IN
(
SELECT MIN(employee_id)
FROM employee) ;


SELECT *
FROM employee
WHERE employee_id IN
(SELECT MAX(employee_id)
FROM employee) ;


-- Write a query to get even and odd record from the query

SELECT *
FROM employee
WHERE MOD(employee_id,2) = 0 ;

SELECT *
FROM employee
WHERE MOD(employee_id,2) = 1
