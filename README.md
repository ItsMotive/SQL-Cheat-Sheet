# SQL-Cheat-Sheet
A repository to recall commonly used SQL commands.

# Table of Contents
- [Definitions](#definitions)
- [Commands](#commands)
  - [SELECT](#select)
  - [FROM](#from)
  - [INSERT](#insert)
  - [UPDATE](#update)
  - [DELETE](#delete)
- [Basic Queries](#basic-queries)
  - [SELECT](#select-1)
  - [WHERE](#where)
  - [ORDER BY](#order-by)
  - [LIMIT](#limit)
  - [OFFSET](#offset)
    - [Basic Pagination](#basic-pagination)
    - [Skipping Rows](#skipping-rows)
- [Advanced Queries](#advanced-queries)
  - [Example Tables](#example-tables)
  - [Joins](#joins)
    - [INNER JOIN](#inner-join)
    - [LEFT JOIN](#left-join-or-left-outer-join)
    - [RIGHT JOIN](#RIGHT-JOIN-or-RIGHT-OUTER-JOIN)
    - [FULL JOIN](#FULL-JOIN-or-FULL-OUTER-JOIN)
    - [CROSS JOIN](#CROSS-JOIN)
    - [SELF JOIN](#SELF-JOIN)
  - [Subqueries](#subqueries)
    - [Types](#types)
    - [Using SELECT](#using-select)
    - [Using FROM](#using-from)
    - [Using WHERE](#using-where)
    - [Using HAVING](#using-having)
    - [Correlated](#correlated)
  - [UNION](#union)
  - [UNION ALL](#union-all)
  - [INTERCEPT](#intercept)
  - [EXCEPT](#except)
- [Examples](#examples)
       

# Definitions
### SQL
- Structured Query Language
- Used for managing and manipulating relational databases

# Commands
- ### SELECT
  - Assigns what columns the query will return
- ### FROM
  - Assigns the table to be used
- ### INSERT
  - Adds new records to table
- ### UPDATE
  - Modifies existing records
- ### DELETE
  - Removes record from table

# Basic Queries
- ### SELECT
  - This will select all columns
  ```
  SELECT * FROM table_name
  ```

- ### WHERE
  - This will select all columns with certain conditions
  ```
  SELECT * FROM table_name
  WHERE column = value
  ```

- ### ORDER BY
  - Orders the query output
  - Sort order can be:
    - Ascending : ASC
    - DESC : DESC
  ```
  SELECT * FROM table_name
  ORDER BY column_name ASC
  ```

- ### LIMIT
  - This will limit the amount of outputs from the query
  ```
  SELECT * FROM table_name
  LIMIT number
  ```

- ### OFFSET
  - Used to skip a specified number of rows before beginning to return the rows from the query. It is commonly used in conjunction with the LIMIT (or FETCH) clause to implement pagination in a result set.
  
  products
  product_id | product_name | price
  --- | --- | --- |
  1 | Product A | 10.00
  2 | Product B | 20.00
  3 | Product C | 30.00
  4 | Product D | 40.00
  5 | Product E | 50.00

    - ### Basic Pagination
    ```
    SELECT product_id, product_name, price
    FROM products
    ORDER BY product_id
    OFFSET 2 ROWS
    FETCH NEXT 2 ROWS ONLY;
    ```
    Results:
    product_id | product_name | price
    --- | --- | --- |
    4 | Product D | 40.00
    5 | Product E | 50.00

    - ### Skipping Rows
    ```
    SELECT product_id, product_name, price
    FROM products
    ORDER BY product_id
    OFFSET 3 ROWS;
    ```
    Results:
    product_id | product_name | price
    --- | --- | --- |
    4 | Product D | 40.00
    5 | Product E | 50.00

# Advanced Queries

### Example Tables: 

employee
employee_id | employee_name | dept_id
--- | --- | --- | 
1 | John Doe | 101
2 | Jane Smith | 102
3 | Alice Jones | 101
4 | Bob Brown | 103

departments
dept_id | dept_name
--- | --- |
101 | HR 
102 | Engineering
104 | Sales

salaries
employee_id | salary
--- | --- |
1 | 50000 
2 | 60000
3 | 55000
4 | 70000

- ### Joins
  - #### INNER JOIN
    - Returns only the rows that have matching values in both tables.
    ```
    SELECT employees.employee_name, departments.dept_name
    FROM employees
    INNER JOIN departments
    ON employees.dept_id = departments.dept_id;
    ```
    Result:
    employee_name | dept_name
    --- | --- |
    John Doe | HR
    Alice Jones | HR
    Jane Smith | Engineering
    
  - ### LEFT JOIN (or LEFT OUTER JOIN)
    - Returns all rows from the left table, and the matched rows from the right table. If no match is found, NULL values are returned for columns from the right table.
    ```
    SELECT employees.employee_name, departments.dept_name
    FROM employees
    LEFT JOIN departments
    ON employees.dept_id = departments.dept_id;
    ```
    Result:
    employee_name | dept_name
    --- | --- |
    John Doe | HR
    Alice Jones | HR
    Jane Smith | Engineering
    Bob Brown | NULL
    
  - ### RIGHT JOIN (or RIGHT OUTER JOIN)
    - Returns all rows from the right table, and the matched rows from the left table. If no match is found, NULL values are returned for columns from the left table.
    ```
    SELECT employees.employee_name, departments.dept_name
    FROM employees
    RIGHT JOIN departments
    ON employees.dept_id = departments.dept_id;
    ```
    Result:
    employee_name | dept_name
    --- | --- |
    John Doe | HR
    Alice Jones | HR
    Jane Smith | Engineering
    NULL | Sales
    
  - ### FULL JOIN (or FULL OUTER JOIN)
    - Returns all rows when there is a match in either left or right table. If there is no match, the result is NULL on the side that does not have a match.
    ```
    SELECT employees.employee_name, departments.dept_name
    FROM employees
    FULL OUTER JOIN departments
    ON employees.dept_id = departments.dept_id;
    ```
    Result:
    employee_name | dept_name
    --- | --- |
    John Doe | HR
    Alice Jones | HR
    Jane Smith | Engineering
    Bob Brown | NULL
    NULL | Sales
    
  - ### CROSS JOIN
    - Returns the Cartesian product of the two tables, i.e., it returns all possible combinations of rows from the two tables.
    ```
    SELECT employees.employee_name, departments.dept_name
    FROM employees
    CROSS JOIN departments;
    ```
    Result:
    employee_name | dept_name
    --- | --- |
    John Doe | HR
    John Doe | Engineering
    John Doe | Sales
    Jane Smith | HR
    Jane Smith | Engineering
    Jane Smith | Sales
    Alice Jones | HR
    Alice Jones | Engineering
    Alice Jones | Sales
    Bob Brown | HR
    Bob Brown | Engineering
    Bob Brown | Sales
    
  - ### SELF JOIN
    - A regular join, but the table is joined with itself. This can be useful to compare rows within the same table.
    ```
    SELECT e1.employee_name AS Employee1, e2.employee_name AS Employee2, e1.dept_id
    FROM employees e1
    INNER JOIN employees e2
    ON e1.dept_id = e2.dept_id
    AND e1.employee_id < e2.employee_id;
    ```
    Result:
    Employee1 | Employee2 | dept_id
    --- | --- | --- |
    John Doe | Alice Jones | 101

- ### Subqueries
  - Known as inner queries or nested queries, are queries within another SQL query. They are used to perform operations that depend on the results of another query. Subqueries can be placed in various parts of an SQL statement.
    
  - ### Types
    - Scalar : Returns single value
    - Row : Returns one row with one or more columns
    - Column : Returns a single column of data, usually used with operators like IN
    - Table : Returns a set that can act as a table
      
  - ### Using Select
    ```
    SELECT employee_name, 
      (SELECT salary 
        FROM salaries 
        WHERE employees.employee_id = salaries.employee_id) AS employee_salary
    FROM employees;
    ```
    Result:
    employee_name | employee_salary
    --- | --- |
    John Doe  | 50000 
    Alice Jones | 60000
    Jane Smith | 55000
    Bob Brown | 70000

  - ### Using WHERE
    ```
    SELECT employee_name 
    FROM employees
    WHERE employee_id IN (SELECT employee_id 
                 FROM salaries 
                 WHERE salary > (SELECT AVG(salary) FROM salaries));
    ```
    Result:
    employee_name |
    --- |
    Jane Smith  
    Bob Brown

  - ### Using FROM
    ```
    SELECT dept_id, AVG(salary) AS avg_salary
    FROM (SELECT employees.dept_id, salaries.salary 
      FROM employees 
      JOIN salaries ON employees.employee_id = salaries.employee_id) AS dept_salaries
    GROUP BY dept_id;
    ```
    Results:
    dept_id | avg_salary
    --- | --- |
    101 | 52500 
    102 | 60000
    103 | 70000

  - ### Using HAVING
    ```
    SELECT dept_id, SUM(salary) AS total_salary
    FROM employees
    JOIN salaries ON employees.emp_id = salaries.emp_id
    GROUP BY dept_id
    HAVING SUM(salary) > (SELECT AVG(total_salary) 
                      FROM (SELECT SUM(salary) AS total_salary 
                            FROM employees 
                            JOIN salaries ON employees.emp_id = salaries.emp_id 
                            GROUP BY dept_id) AS dept_totals);
    ```
    Results:
    dept_id | avg_salary
    --- | --- |
    103 | 70000

  - ### Correlated
    
    - A subquery that references columns from the outer query. It is evaluated once for each row processed by the outer query.
    ```
    SELECT employee_name 
    FROM employees e
    WHERE salary > (SELECT AVG(salary) 
                FROM salaries s 
                WHERE s.dept_id = e.dept_id);
    ```
    Results:
    employee_name | dept_id | salary
    --- | --- | --- |
    Alice Jones | 101 | 55000

- ### UNION
  - Combines the results of two or more SELECT statements and removes duplicate rows from the result set.

  employee_us
  emp_id | emp_name |	country
  --- | --- | --- |
  1	| John Doe | USA
  2	| Jane Smith | USA
  3	| Alice Jones | USA
  
  employee_uk
  emp_id | emp_name | country
  --- | --- | --- |
  4	| Bob Brown | UK
  5	| Charlie Black | UK
  2	| Jane Smith | UK

    ```
    SELECT emp_id, emp_name, country
    FROM employees_us
    UNION
    SELECT emp_id, emp_name, country
    FROM employees_uk;
    ```
    Result:
    emp_id | emp_name	| country
    --- | --- | --- |
    1	| John Doe |USA
    2	| Jane Smith | USA
    3	| Alice Jones | USA
    4	| Bob Brown | UK
    5	| Charlie Black | UK

- ### UNION ALL
  - Combines the results of two or more SELECT statements and includes all rows, including duplicates.
    ```
    SELECT emp_id, emp_name, country
    FROM employees_us
    UNION ALL
    SELECT emp_id, emp_name, country
    FROM employees_uk;
    ```
    Result:
    emp_id | emp_name	| country
    --- | --- | --- |
    1	| John Doe |USA
    2	| Jane Smith | USA
    3	| Alice Jones | USA
    4	| Bob Brown | UK
    5	| Charlie Black | UK
    2 | Jane Smith | UK

- ### INTERSECT
  - Returns the common rows from two SELECT statements, meaning it returns only the rows that are present in both result sets.

  employees_current
  emp_id | emp_name | country
  --- | --- | --- |
  1	| John Doe | USA
  2	| Jane Smith | USA
  3	| Alice Jones | USA
  4	| Bob Brown | UK

  employees_previous
  emp_id | emp_name | country
  --- | --- | --- |
  2 | Jane Smith | USA
  3	| Alice Jones | USA
  5	| Charlie Black	| UK

  ```
  SELECT emp_id, emp_name, country
  FROM employees_current
  INTERSECT
  SELECT emp_id, emp_name, country
  FROM employees_previous;
  ```
  Result:
  emp_id | emp_name	| country
  --- | --- | --- |
  2	| Jane Smith | USA
  3	| Alice Jones	| USA

- ### EXCEPT
  - Returns the rows from the first SELECT statement that are not present in the second SELECT statement.
    ```
    SELECT emp_id, emp_name, country
    FROM employees_current
    EXCEPT
    SELECT emp_id, emp_name, country
    FROM employees_previous;
    ```
    Result:
    emp_id | emp_name	| country
    --- | --- | --- |
    1	| John Doe | USA
    4	| Bob Brown	| UK


- ### Insert
  - Inserts data into table
  ```
  INSERT INTO table_name (new_column, ...)
  VALUES (value, ...)
  ```

- ### Update
  - Updates row data in table
  ```
  UPDATE table_name
  SET column = value
  WHERE column = value
  ```

- ### Delete
  - Remove row from table
  ```
  DELETE FROM table_name
  WHERE column_name = value
  ```

- ### Create Table
  - Creates a new table
  ```
  CREATE TABLE table_name (
        column_name1 INT PRIMARY KEY
        column_name2 VARCHAR(50) NOT NULL
  )
  ```

# Examples
- ### SELF JOIN/CTE (Common Table Expression) Example

  Weather:
   id | recordDate | temperature |
  --- |--- | --- |
  | 1  | 2015-01-01 | 10
  | 2  | 2015-01-02 | 25
  | 3  | 2015-01-03 | 20
  | 4  | 2015-01-04 | 30
  
  - Write a solution to find all dates' Id with higher temperatures compared to its previous dates (yesterday).
  ```
  WITH WeatherCTE AS(
      SELECT 
          id, 
          recordDate, 
          temperature,
          ROW_NUMBER() OVER (ORDER BY recordDate) as rn
      FROM Weather
  )
  SELECT w2.id as Id
  FROM WeatherCTE as w1
  INNER JOIN WeatherCTE as w2
  ON w1.rn = w2.rn - 1
  WHERE w2.temperature > w1.temperature
  ```
  Result: 
  | Id |
  | --- |
  | 2  |
  | 4  |

  - Explanation
    ```
    WITH WeatherCTE AS(
        SELECT 
            id, 
            recordDate, 
            temperature,
            ROW_NUMBER() OVER (ORDER BY recordDate) as rn
        FROM Weather
    )
    ```
    This will create a CTE of the existing table. ROW_NUMBER() creates a sequential integer to each row. OVER(ORDER BY) orders column.
    ```
    SELECT w2.id as Id
    FROM WeatherCTE as w1
    INNER JOIN WeatherCTE as w2
    ON w1.rn = w2.rn - 1
    WHERE w2.temperature > w1.temperature
    ```
    SELF JOIN to compare the row number. Checks to see if entry_2.row_number is greater than entry_1.row_number. 
