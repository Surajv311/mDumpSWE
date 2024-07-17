
# SQL Functions


- Joins in SQL: INNER JOIN, LEFT JOIN, RIGHT JOIN, FULL JOIN. Syntax: `SELECT table1.column1,table1.column2,table2.column1,.... FROM table1 JOIN table2 ON table1.matching_column = table2.matching_column;`. Here, table1: First table, table2: Second table, matching_column: Column common to both the tables.
- Order of execution in SQL: 

```
FROM [MyTable]
ON [MyCondition]
JOIN [MyJoinedTable]
WHERE [...]
GROUP BY [...]
HAVING [...]
SELECT [...]
ORDER BY [...]
```

- Aggregate Functions in sql: COUNT(), SUM(), AVG(), MIN(), MAX().
- Window/ Analytic Functions in sql: ORDER BY, PARTITION BY, RANK(), DENSE_RANK(), ROW_NUMBER(), LEAD(), LAG(). [Window functions sql example _vl](https://www.youtube.com/watch?v=Ww71knvhQ-s&ab_channel=techTFQ). 

Example for SQL Syntax, Aggregate, Window functions;

First: SQL Syntax, Aggregate Functions:

- `SELECT column1, column2, ... FROM table_name;`
- `SELECT column1, column2, ... FROM table_name WHERE condition;`
- `SELECT column1, column2, ... FROM table_name ORDER BY column1 [ASC|DESC], column2 [ASC|DESC], ...;`
- `SELECT column1, aggregate_function(column2) FROM table_name GROUP BY column1;`
  - Eg: SELECT department, AVG(salary) FROM employees GROUP BY department;
  - The GROUP BY clause is used in conjunction with aggregate functions (like SUM(), COUNT(), AVG(), etc.) to group the result set into summary rows. Eg: 
  - We can have multiple SELECT and GROUP BY clauses in a single SQL query: `SELECT department, job_title, AVG(salary) AS avg_salary, COUNT(*) AS num_employees FROM employees GROUP BY department, job_title ORDER BY department, avg_salary DESC;`. When you have multiple GROUP BY clauses, the grouping is performed in the order the columns are listed in the GROUP BY clause. The first column in the GROUP BY clause is used to create the initial groups, then the second column is used to further sub-group the results within each of the first-level groups, and so on.

Sample table before group by: 

| employee_id | first_name | last_name | department | salary |
|-------------|------------|-----------|------------|--------|
| 1           | John       | Doe       | IT         | 70000  |
| 2           | Jane       | Smith     | IT         | 60000  |
| 3           | Bob        | Johnson   | Marketing  | 55000  |
| 4           | Sarah      | Lee       | Marketing  | 50000  |
| 5           | Tom        | Wilson    | Sales      | 45000  |
| 6           | Emily      | Davis     | Sales      | 40000  |

Post running query: `SELECT department, AVG(salary) FROM employees GROUP BY department;`

| department | avg_salary |
|------------|------------|
| IT         | 65000.00   |
| Marketing  | 52500.00   |
| Sales      | 42500.00   |

- `SELECT column1, aggregate_function(column2) FROM table_name GROUP BY column1 HAVING condition;`
  - Eg: SELECT department, AVG(salary) FROM employees GROUP BY department HAVING AVG(salary) > 50000;
  - The difference between the having and where clause in SQL is that the where clause cannot be used with aggregates, but the having clause can.
- `SELECT column1, column2, ... FROM table_name LIMIT offset, row_count;`
  - Eg: select * from cycles_table limit 10 offset 5; This query selects all columns from the cycles_table, limiting the results to 10 rows starting from the sixth row (offset 5).
- `SELECT DISTINCT column1, column2, ... FROM table_name;`
- `SELECT column1, column2, ... FROM table1 JOIN table2 ON table1.column = table2.column;`
- `INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...);`
  - Eg: INSERT INTO employees (first_name, last_name, email, department) VALUES ('John', 'Doe', 'john.doe@example.com', 'IT');
- `UPDATE table_name SET column1 = value1, column2 = value2, ... WHERE condition;`
  - Eg: UPDATE employees SET salary = 60000 WHERE employee_id = 123;
- `DELETE FROM table_name WHERE condition;`
- `SELECT column1, column2, ... FROM table_name WHERE column LIKE pattern;`
  - Eg: SELECT first_name, last_name FROM employees WHERE first_name LIKE 'J%';
  - The LIKE operator is used in a WHERE clause to search for a specified pattern in a column. There are two wildcards often used in conjunction with the LIKE operator: The percent sign % represents zero, one, or multiple characters and; The underscore sign _ represents one, single character. Eg: SELECT * FROM Customers WHERE city LIKE 'L_nd__';
- `SELECT column1, column2, ... FROM table_name WHERE column IN (value1, value2, ...);`
- `SELECT column1, column2, ... FROM table_name WHERE column BETWEEN value1 AND value2;`
  - Eg: SELECT first_name, last_name, salary FROM employees WHERE salary BETWEEN 50000 AND 80000;
- `SELECT column1, column2, ... FROM table_name WHERE column IS NULL;`
- `SELECT column1, column2, ... FROM table_name WHERE column IS NOT NULL;`

Second: Window Functions:

Consider a table named employees with the following data:

| emp_id | emp_name | department |
| :----: | :------: | :--------: |
|   1    |  Alice   |     HR     |
|   1    |   Bob    |     HR     |
|   1    | Charlie  |   Sales    |
|   1    |  David   |   Sales    |
|   1    |   Eve    | Marketing  |

For: `SELECT emp_name, department, RANK() OVER (ORDER BY department) AS dept_rank FROM employees;`
`RANK()`: RANK() is a window function that assigns a unique rank to each row within the partition of a result set. It assigns the same rank to rows with the same values and leaves gaps between ranks when there are ties.
Output: 

| emp_id  | emp_name  | dept_rank |
| :-----: | :-------: | :-------: |
|  Alice  |    HR     |     1     |
|   Bob   |    HR     |     1     |
| Charlie |   Sales   |     3     |
|  David  |   Sales   |     3     |
|   Eve   | Marketing |     5     |

For: `SELECT emp_name, department, DENSE_RANK() OVER (ORDER BY department) AS dept_dense_rank FROM employees;`
`DENSE_RANK()`: DENSE_RANK() is similar to RANK() but it doesn't leave gaps between ranks when there are ties. It assigns consecutive ranks to rows with the same values, so there are no gaps in the ranking sequence.
Output: 

| emp_id  | emp_name  | dept_dense_rank |
| :-----: | :-------: | :-------------: |
|  Alice  |    HR     |        1        |
|   Bob   |    HR     |        1        |
| Charlie |   Sales   |        2        |
|  David  |   Sales   |        2        |
|   Eve   | Marketing |        3        |

For: `SELECT emp_name, department, ROW_NUMBER() OVER (ORDER BY emp_name) AS row_num FROM employees;`
`ROW_NUMBER()`: ROW_NUMBER() is a window function that assigns a unique sequential integer to each row within the partition of a result set. It does not handle ties; each row receives a distinct number, starting from 1 and incrementing by 1 for each row.
Output: 

| emp_id  | emp_name  | row_num |
| :-----: | :-------: | :-----: |
|  Alice  |    HR     |    1    |
|   Bob   |    HR     |    2    |
| Charlie |   Sales   |    3    |
|  David  |   Sales   |    4    |
|   Eve   | Marketing |    5    |

For: `SELECT emp_name, department, RANK() OVER () AS rank_all FROM employees;`
`OVER()`: OVER() is a clause used with window functions to define the window or set of rows that the function operates on. It specifies the partitioning and ordering of the rows in the result set for the window function to process. If used without any specific partitioning or ordering, it considers the entire result set as a single partition.
Output: 

| emp_id  | emp_name  | rank_all |
| :-----: | :-------: | :------: |
|  Alice  |    HR     |    1     |
|   Bob   |    HR     |    1     |
| Charlie |   Sales   |    3     |
|  David  |   Sales   |    3     |
|   Eve   | Marketing |    5     |

For: `SELECT emp_name, department, RANK() OVER (PARTITION BY department ORDER BY emp_name) AS dept_rank FROM employees;`
`OVER() PARTITION BY`: OVER() PARTITION BY is used to partition the result set into distinct subsets (partitions) based on the values of one or more columns. It divides the result set into groups, and the window function is applied separately to each group. Within each partition, the window function operates on the rows based on the specified ordering (or the default ordering if not specified).
Output: 

| emp_id  | emp_name  | dept_rank |
| :-----: | :-------: | :-------: |
|  Alice  |    HR     |     1     |
|   Bob   |    HR     |     2     |
| Charlie |   Sales   |     1     |
|  David  |   Sales   |     2     |
|   Eve   | Marketing |     1     |

For: `SELECT emp_name, department, ROW_NUMBER() OVER (PARTITION BY department ORDER BY emp_name) AS dept_row_num FROM employees;`
`ROW_NUMBER() OVER() PARTITION BY`: ROW_NUMBER() OVER() PARTITION BY combines the functionality of ROW_NUMBER() and OVER() PARTITION BY. It assigns a unique sequential integer to each row within each partition of the result set. The numbering starts from 1 for each partition, and rows are ordered within each partition as specified.
Output: 

| emp_id  | emp_name  | dept_row_num |
| :-----: | :-------: | :----------: |
|  Alice  |    HR     |      1       |
|   Bob   |    HR     |      2       |
| Charlie |   Sales   |      1       |
|  David  |   Sales   |      2       |
|   Eve   | Marketing |      1       |

For: `SELECT emp_name, department, ROW_NUMBER() OVER (PARTITION BY department ORDER BY emp_name) AS dept_row_num FROM employees;`
`ROW_NUMBER() OVER PARTITION BY ORDER BY`: Similar to ROW_NUMBER() OVER() PARTITION BY, but with an added ORDER BY clause. It assigns a unique sequential integer to each row within each partition, ordered by the specified column(s). The numbering starts from 1 for each partition, and rows are ordered within each partition according to the specified ordering.
Output: 

| emp_id  | emp_name  | dept_row_num |
| :-----: | :-------: | :----------: |
|  Alice  |    HR     |      1       |
|   Bob   |    HR     |      2       |
| Charlie |   Sales   |      1       |
|  David  |   Sales   |      2       |
|   Eve   | Marketing |      1       |

- SQL UPSERT command: It’s “update” and “insert.” In the context of relational databases, an upsert is a database operation that will update an existing row if a specified value already exists in a table, and insert a new row if the specified value doesn't already exist.
- SQL clause "GROUP BY 1" mean: It means to group by the first column of your result set regardless of what it's called. You can do the same with ORDER BY.
- SQL CHECK constraint: It is used to specify the condition that must be validated in order to insert data into a table. Eg: 

```
CREATE TABLE Orders (
order_id INT PRIMARY KEY, amount INT CHECK (amount > 0));
```

- Keys in SQL: 
  - A **primary key** uniquely identifies each record in a database table. Any individual key that does this can be called a **candidate key**, but only one can be chosen by database engineers as a primary key. 
  - A **composite key** is composed of two or more attributes that collectively uniquely identify each record. 
  - A **foreign key** in a database table is taken from some other table and applied in order to link database records back to that foreign table. The foreign key in the database table where it resides is actually the primary key of the other table.
  - For more details, my notes: [cs_core_notes _al](https://github.com/Surajv311/myCS-NOTES/blob/main/CS_CORE-NOTES/DBMS/dbms%20(5).jpg)
- `SELECT CURRENT_TIMESTAMP()` - Return the current date and time. 
- The `TRUNCATE` statement removes all data from a table but leaves the table structure intact. The `DELETE` statement is used to remove rows from a table one by one. The `DROP` statement deletes the entire table, including all data and the table structure. [difference truncate, delete, drop _al](https://stackoverflow.com/questions/32499763/what-is-the-difference-between-truncate-drop-and-delete-of-tables-and-when-to)
- LIKE Operator: We use the SQL LIKE operator with the WHERE clause to get a result set that matches the given string pattern. Eg: `SELECT * FROM Customers WHERE country LIKE 'UK';`
- `WITH` Clause: A WITH clause defines a temporary data set whose output is available to be referenced in subsequent queries. Eg: 

```
WITH cte_quantity
AS
(SELECT
    SUM(Quantity) as Total
FROM OrderDetails
GROUP BY ProductID) 
SELECT
    AVG(Total) average_product_quantity
FROM cte_quantity;
```

- Order of execution of ORDER BY and LIMIT in a MySQL query: A SQL LIMIT will in all databases always work on the result of a query, so it will first run the query with the ORDER BY and that result will then be limited.
  - If the query has not got any specific ordering, it returns the first 10 rows it receives. But if there is a "WHERE ..." or "ORDER BY ..." clause, it must first get the full resultset and then fetch the first 10 rows. [Limit clause _al](https://dba.stackexchange.com/a/62444)
- ORDER BY: sort the data in ascending or descending order; GROUP BY: arrange identical data into groups. It allows you to perform aggregation functions on non-grouped columns (such as SUM, COUNT, AVG, etc).
- PARTITION BY and GROUP BY difference: PARTITION BY is analytic, while GROUP BY is aggregate. In order to use PARTITION BY, you have to contain it with an OVER clause.
  - GROUP BY modifies the entire query, like: `select customerId, count(*) as orderCount from Orders group by customerId`
    - GROUP BY normally reduces the number of rows returned by rolling them up and calculating averages or sums for each row.
  - But PARTITION BY just works on a window function, like ROW_NUMBER(): `select row_number() over (partition by customerId order by orderId) as OrderNumberForThisCustomer from Orders`
    - PARTITION BY does not affect the number of rows returned, but it changes how a window function's result is calculated.
  - [SQL Window Functions good reference 1 _vl](https://www.youtube.com/watch?v=Ww71knvhQ-s), [SQL Window Functions good reference 2 _vl](https://www.youtube.com/watch?v=KwEjkpFltjc)
- [SQL Query plan internals _al](https://www.red-gate.com/simple-talk/databases/sql-server/performance-sql-server/execution-plan-basics/)
- Scalar vs Predicate Queries: 
  - Scalar: A scalar subquery is a subquery that returns exactly one value (one row with one column). This type of subquery is often used in places where a single value is expected, such as in the SELECT clause, WHERE clause, or HAVING clause.
    - Eg: `SELECT employee_id, first_name, last_name FROM employees WHERE salary > (SELECT AVG(salary) FROM employees);`
  - Predicate: A predicate subquery is a subquery that is used as part of a predicate (a condition that evaluates to true or false) in the WHERE or HAVING clause. These subqueries can return multiple values and are often used with operators like IN, ANY, ALL, or EXISTS.
    - Eg: `SELECT employee_id, first_name, last_name FROM employees WHERE department_id IN (SELECT department_id FROM departments WHERE location_id = 1700);`
  - Scalar subqueries return a single value (one row, one column). Predicate subqueries can return multiple rows and columns, but they are used in conditions that evaluate to true or false.
- 
- 
- 

----------------------------------------------------------------------

SQL Questions:

Write a solution to find the employees who earn more than their managers.
Input: 
Employee table:
+----+-------+--------+-----------+
| id | name  | salary | managerId |
+----+-------+--------+-----------+
| 1  | Joe   | 70000  | 3         |
| 2  | Henry | 80000  | 4         |
| 3  | Sam   | 60000  | Null      |
| 4  | Max   | 90000  | Null      |
+----+-------+--------+-----------+
Output: 
+----------+
| Employee |
+----------+
| Joe      |
+----------+
Explanation: Joe is the only employee who earns more than his manager.
SELECT e2.name as Employee FROM employee e1 INNER JOIN employee e2 ON e1.id = e2.managerID WHERE e1.salary < e2.salary

Q2


----------------------------------------------------------------------

