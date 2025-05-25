# B5-Assignment-2


1. What is PostgreSQL?

PostgreSQL is an open-source, powerful, and object-relational database management system (ORDBMS). It extends the SQL language with many advanced features such as:

* Complex queries
* Foreign keys
* Triggers
* Updatable views
* Transactional integrity
* Multiversion concurrency control (MVCC)

PostgreSQL supports both structured (SQL) and semi-structured (JSON/XML) data. It is known for its standards compliance, extensibility and robust community. You can define your own data types, operators, aggregate functions, and more.

Use Case Example:
If you're building a web app where you need ACID-compliant transactions, such as banking software, PostgreSQL ensures your data is consistent and secure.


2. What is the purpose of a database schema in PostgreSQL?

A schema in PostgreSQL is a logical container or namespace for database objects like tables, views, functions, types, and indexes.

Purpose of Schema:

* Organize data logically within the same database
* Avoid naming collisions (e.g., two tables with the same name in different schemas)
* Manage permissions and access control
* Help with modular design and multi-tenant applications

Example:
CREATE SCHEMA sales;

CREATE TABLE sales.orders (
    order_id SERIAL PRIMARY KEY,
    amount NUMERIC
);


Here, the `orders` table belongs to the `sales` schema, isolating it from other tables with the same name.

3. Explain the Primary Key and Foreign Key concepts in PostgreSQL.
Primary Key:
A primary key uniquely identifies each row in a table. It:

* Must contain unique values
* Cannot be NULL
* Automatically creates a unique index

Example:
CREATE TABLE customers (
    customer_id SERIAL PRIMARY KEY,
    name TEXT
);


Foreign Key:
A foreign key establishes a relationship between two tables, linking a column in one table to the primary key in another.

Example:
CREATE TABLE orders (
    order_id SERIAL PRIMARY KEY,
    customer_id INT REFERENCES customers(customer_id),
    order_date DATE
);
This means each `order` must be linked to a valid `customer`.



4. What is the difference between the `VARCHAR` and `CHAR` data types?

Both `VARCHAR` and `CHAR` are used to store character strings, but they behave differently:

| Feature       | `VARCHAR(n)`                | `CHAR(n)`                         |
| ------------- | --------------------------- | --------------------------------- |
| Meaning       | Variable-length string      | Fixed-length string               |
| Storage       | Stores only used characters | Pads unused space with spaces     |
| Efficiency    | More space-efficient        | Slightly faster for fixed lengths |
| Usage Example | `VARCHAR(50)` for names     | `CHAR(2)` for country codes       |

Example:
CREATE TABLE products (
    code CHAR(5),
    name VARCHAR(100)
);


In this table:

* `code` will always store exactly 5 characters, padded if needed.
* `name` can be up to 100 characters, with variable length.


5. Explain the purpose of the `WHERE` clause in a `SELECT` statement.

The `WHERE` clause filters records based on specific conditions. It ensures that only rows meeting the criteria are returned.

Syntax:
SELECT * FROM employees
WHERE department = 'HR';

This query retrieves all employees only from the HR department.




6. What are the `LIMIT` and `OFFSET` clauses used for?

These clauses are essential for pagination and data sampling.

* `LIMIT` restricts the number of rows returned.
* `OFFSET` skips a number of rows before starting to return rows.

Example:
SELECT * FROM products
ORDER BY product_id
LIMIT 10 OFFSET 20;


This returns 10 products starting from the 21st row in the result set.

Use Case:Useful in web apps for paginating results (e.g., show 10 items per page).


7. How can you modify data using `UPDATE` statements?

The `UPDATE` statement is used to change existing values in a table.

Syntax:
UPDATE table_name
SET column1 = value1, column2 = value2
WHERE condition;

Example:
UPDATE employees
SET salary = salary * 1.10
WHERE department = 'Sales';
```

This increases the salary of all employees in the Sales department by 10%.

Always include a `WHERE` clause to avoid updating **all** rows unintentionally.


8. What is the significance of the `JOIN` operation, and how does it work in PostgreSQL?

JOINs allow combining data from multiple tables based on a related column, making relational databases powerful and scalable.

 Types of JOINs:

* INNER JOIN: Returns only matching rows.
* LEFT JOIN: All rows from the left table, with matches from the right table.
* RIGHT JOIN: Opposite of LEFT JOIN.
* FULL JOIN: All rows from both tables; NULL if no match.

Example (INNER JOIN):
SELECT customers.name, orders.order_date
FROM customers
INNER JOIN orders ON customers.customer_id = orders.customer_id;


This returns customer names with their respective order dates.

JOINs are critical for normalization and multi-table queries.


9. Explain the `GROUP BY` clause and its role in aggregation operations.

The `GROUP BY` clause groups rows that have the same values in specified columns, and allows you to **apply aggregate functions** like `SUM`, `COUNT`, `AVG`, etc.

Example:

SELECT department, AVG(salary)
FROM employees
GROUP BY department;

This calculates the average salary in each department.


10. How can you calculate aggregate functions like `COUNT()`, `SUM()`, and `AVG()` in PostgreSQL?

Aggregate functions perform calculations on a set of values:

* `COUNT()` – Returns the number of rows.
* `SUM()` – Adds up numeric values.
* `AVG()` – Calculates average value.
* `MIN()`, `MAX()` – Get the smallest/largest value.

Example:
SELECT
    COUNT(*) AS total_employees,
    SUM(salary) AS total_salary,
    AVG(salary) AS average_salary
FROM employees;


These functions give a summary of employee salaries.



