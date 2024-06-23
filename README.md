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
  - [SELECT](#select)
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

# Definitions
## SQL
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
    
  - LEFT JOIN (or LEFT OUTER JOIN)
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
    
  - RIGHT JOIN (or RIGHT OUTER JOIN)
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
    
  - FULL JOIN (or FULL OUTER JOIN)
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
    
  - CROSS JOIN
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
    
  - SELF JOIN
    - A regular join, but the table is joined with itself. This can be useful to compare rows within the same table.
    ```
    SELECT e1.employee_name AS Employee1, e2.employee_name AS Employee2, e1.dept_id
    FROM employees e1
    INNER JOIN employees e2
    ON e1.dept_id = e2.dept_id
    AND e1.employee_id < e2.employee_id;
    ```
    Employee1 | Employee2 | dept_id
    --- | --- | --- |
    John Doe | Alice Jones | 101

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

