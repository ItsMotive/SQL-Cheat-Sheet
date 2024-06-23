# SQL-Cheat-Sheet
A repository to recall commonly used SQL commands.

# Table of Contents

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
- ### Select
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

# Advanced SQL Queries

Example Tables: 

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
  - INNER JOIN
    - An INNER JOIN returns only the rows that have matching values in both tables
    ```
    SELECT * FROM table_name
    ```
    
  - LEFT JOIN (or LEFT OUTER JOIN)
    ```
    SELECT * FROM table_name
    ```
    
  - RIGHT JOIN (or RIGHT OUTER JOIN)
    ```
    SELECT * FROM table_name
    ```
    
  - FULL JOIN (or FULL OUTER JOIN)
    ```
    SELECT * FROM table_name
    ```
    
  - CROSS JOIN
    ```
    SELECT * FROM table_name
    ```
    
  - SELF JOIN
    ```
    SELECT * FROM table_name
    ```


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

