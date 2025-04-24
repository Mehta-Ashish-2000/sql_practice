/* Sales company data is used for the analysis
The database named **"employees"** containing tables related to employee management. 
These include employee details, departments, department assignments, managers, salaries and sales data.*/

#select schema/ database
USE employees;

#demonstrate SELECT, FROM & WHERE clause
SELECT 
    emp_no, first_name, last_name
FROM
    employees
WHERE
    gender = 'M';

#use "*" amd ORDER BY clause
SELECT 
    *
FROM
    employees
ORDER BY hire_date DESC;

#use of GROUP BY function
SELECT 
    COUNT(gender)
FROM
    employees
GROUP BY gender;

#uses of different type of joins in queries
SELECT 
    e.emp_no, e.first_name, e.last_name, s.salary
FROM
    employees AS e
        INNER JOIN
    salaries AS s ON e.emp_no = s.emp_no;

SELECT 
    *
FROM
    employees AS e
        LEFT JOIN
    salaries AS s ON e.emp_no = s.emp_no;

SELECT 
    *
FROM
    employees AS e
        RIGHT JOIN
    salaries AS s ON e.emp_no = s.emp_no;

#demonstrate the use of subqueries in MySql
SELECT 
    first_name, last_name
FROM
    employees
WHERE
    (SELECT 
            emp_no
        FROM
            dept_manager
        WHERE
            employees.emp_no = dept_manager.emp_no);

#use of aggregate functions (SUM, AVG, MIN, MAX)
SELECT 
    MIN(salary)
FROM
    salaries;

SELECT 
    MAX(salary)
FROM
    salaries;

SELECT 
    SUM(salary)
FROM
    salaries;

SELECT 
    AVG(salary)
FROM
    salaries;

#creating views in MySql
#the purpose of creating views is to simplify complex queries.
#It doesn’t store data itself but shows data from one or more tables through a saved query.
CREATE OR REPLACE VIEW gender_average_salary AS
    (SELECT 
        a.gender, AVG(b.salary)
    FROM
        employees AS a
            JOIN
        salaries AS b ON a.emp_no = b.emp_no
    WHERE
        hire_date > '2000-01-01'
    GROUP BY a.gender);

#An index is like a table of contents for your database, it makes searching faster. 
#It helps SQL find rows quicker, especially in large tables.
SELECT 
    *
FROM
    employees
WHERE
    emp_no BETWEEN 10001 AND 10078;
#creating index from above query
CREATE INDEX id_emp_no ON employees(emp_no);

