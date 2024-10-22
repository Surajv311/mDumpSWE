
# SQL Functions


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

----------------------------------------------------------------------

Example for SQL Syntax, Aggregate, Window functions;

First: SQL Syntax, Aggregate Functions:

- `SELECT column1, column2, ... FROM table_name;`
  - This also works: SELECT table_name.column1, table_name.column2, ... FROM table_name;
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
- `SELECT column1, column2, ... FROM table1 JOIN table2 ON table1.column = table2.column;` - Note the table1 and table2. 
  - INNER JOIN: Returns records that have matching values in both tables.
  - LEFT JOIN: Returns all records from the left table and the matched records from the right table. The result is NULL from the right side if there is no match.
  - RIGHT JOIN: Returns all records from the right table and the matched records from the left table. The result is NULL from the left side if there is no match.
  - FULL JOIN: Returns all records when there is a match in either left or right table. The result is NULL from the side where there is no match.
  - CROSS/CARTESIAN JOIN: Returns the Cartesian product of the two tables, i.e., it returns all possible combinations of rows from the two tables.
  - SELF JOIN: A regular join but the table is joined with itself.
  - NATURAL JOIN: A type of INNER JOIN where the join is implicitly based on all columns in the two tables that have the same name.
  - Other eg, we can have multiple conditions in ON statement: SELECT t1.column1, t1.column2, t2.column3, t2.column4 FROM table1 t1 INNER JOIN table2 t2 ON t1.key1 = t2.key1 AND t1.key2 = t2.key2 AND t1.date BETWEEN '2022-01-01' AND '2022-12-31'.
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
- `CREATE TABLE table_name( column1 datatype, column2 datatype, column3 datatype, PRIMARY KEY( one or more columns ) );`
- `CREATE INDEX index_name ON table_name ( column1, column2,...columnN);`
  - Indexes are special lookup tables that the database search engine can use to speed up data retrieval. An index is a pointer to data in a table.
  - We have simple, unique, composite indexes, etc. 
- `SELECT column1, column2 FROM table1 UNION SELECT column1, column2 FROM table2;`
  - The SQL UNION clause is used to combine the results of two or more SELECT statements into a single result set. The UNION operator selects only distinct values by default, meaning it removes duplicates. If you want to include duplicates, you can use the UNION ALL operator. We also have other clauses like Intersect, Except, etc. 
- `TRUNCATE TABLE table_name;`
- `CREATE VIEW view_name AS SELECT column1, column2..... FROM table_name WHERE [condition];`
- `ALTER TABLE table_name [ADD|DROP|MODIFY] column_name [data_ype];`
  - Other eg: ALTER TABLE table_name RENAME TO new_table_name;
  - You can also alter table to add primary keys, constraints, etc. 
- `SELECT COALESCE(NULL, NULL, 'Hi', NULL, 'go') from table;`
  - The COALESCE() function returns the first non-null value in a list.
- `CREATE DATABASE database_name;`
- `DROP DATABASE database_name;`
- `USE database_name;`
- `COMMIT;` and/or `ROLLBACK;`, etc. 
- We have SQL date functions like: DAYOFMONTH(), CURRENT_TIMESTAMP(), DATEDIFF(), etc.

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

| emp_name  | department  | dept_rank |
| :-----: | :-------: | :-------: |
|  Alice  |    HR     |     1     |
|   Bob   |    HR     |     1     |
| Charlie |   Sales   |     3     |
|  David  |   Sales   |     3     |
|   Eve   | Marketing |     5     |

For: `SELECT emp_name, department, DENSE_RANK() OVER (ORDER BY department) AS dept_dense_rank FROM employees;`
`DENSE_RANK()`: DENSE_RANK() is similar to RANK() but it doesn't leave gaps between ranks when there are ties. It assigns consecutive ranks to rows with the same values, so there are no gaps in the ranking sequence.
Output: 

| emp_name  | department  | dept_dense_rank |
| :-----: | :-------: | :-------------: |
|  Alice  |    HR     |        1        |
|   Bob   |    HR     |        1        |
| Charlie |   Sales   |        2        |
|  David  |   Sales   |        2        |
|   Eve   | Marketing |        3        |

For: `SELECT emp_name, department, ROW_NUMBER() OVER (ORDER BY emp_name) AS row_num FROM employees;`
`ROW_NUMBER()`: ROW_NUMBER() is a window function that assigns a unique sequential integer to each row within the partition of a result set. It does not handle ties; each row receives a distinct number, starting from 1 and incrementing by 1 for each row.
Output: 

| emp_name  | department  | row_num |
| :-----: | :-------: | :-----: |
|  Alice  |    HR     |    1    |
|   Bob   |    HR     |    2    |
| Charlie |   Sales   |    3    |
|  David  |   Sales   |    4    |
|   Eve   | Marketing |    5    |

For: `SELECT emp_name, department, RANK() OVER () AS rank_all FROM employees;`
`OVER()`: OVER() is a clause used with window functions to define the window or set of rows that the function operates on. It specifies the partitioning and ordering of the rows in the result set for the window function to process. If used without any specific partitioning or ordering, it considers the entire result set as a single partition.
Output: 

| emp_name  | department  | rank_all |
| :-----: | :-------: | :------: |
|  Alice  |    HR     |    1     |
|   Bob   |    HR     |    1     |
| Charlie |   Sales   |    3     |
|  David  |   Sales   |    3     |
|   Eve   | Marketing |    5     |

For: `SELECT emp_name, department, RANK() OVER (PARTITION BY department ORDER BY emp_name) AS dept_rank FROM employees;`
`OVER() PARTITION BY`: OVER() PARTITION BY is used to partition the result set into distinct subsets (partitions) based on the values of one or more columns. It divides the result set into groups, and the window function is applied separately to each group. Within each partition, the window function operates on the rows based on the specified ordering (or the default ordering if not specified).
Output: 

| emp_name  | department  | dept_rank |
| :-----: | :-------: | :-------: |
|  Alice  |    HR     |     1     |
|   Bob   |    HR     |     2     |
| Charlie |   Sales   |     1     |
|  David  |   Sales   |     2     |
|   Eve   | Marketing |     1     |

For: `SELECT emp_name, department, ROW_NUMBER() OVER (PARTITION BY department ORDER BY emp_name) AS dept_row_num FROM employees;`
`ROW_NUMBER() OVER() PARTITION BY`: ROW_NUMBER() OVER() PARTITION BY combines the functionality of ROW_NUMBER() and OVER() PARTITION BY. It assigns a unique sequential integer to each row within each partition of the result set. The numbering starts from 1 for each partition, and rows are ordered within each partition as specified.
Output: 

| emp_name  | department  | dept_row_num |
| :-----: | :-------: | :----------: |
|  Alice  |    HR     |      1       |
|   Bob   |    HR     |      2       |
| Charlie |   Sales   |      1       |
|  David  |   Sales   |      2       |
|   Eve   | Marketing |      1       |

For: `SELECT emp_name, department, ROW_NUMBER() OVER (PARTITION BY department ORDER BY emp_name) AS dept_row_num FROM employees;`
`ROW_NUMBER() OVER PARTITION BY ORDER BY`: Similar to ROW_NUMBER() OVER() PARTITION BY, but with an added ORDER BY clause. It assigns a unique sequential integer to each row within each partition, ordered by the specified column(s). The numbering starts from 1 for each partition, and rows are ordered within each partition according to the specified ordering.
Output: 

| emp_name  | department  | dept_row_num |
| :-----: | :-------: | :----------: |
|  Alice  |    HR     |      1       |
|   Bob   |    HR     |      2       |
| Charlie |   Sales   |      1       |
|  David  |   Sales   |      2       |
|   Eve   | Marketing |      1       |

----------------------------------------------------------------------

- SQL UPSERT command: It’s “update” and “insert”. In the context of relational databases, an upsert is a database operation that will update an existing row if a specified value already exists in a table, and insert a new row if the specified value doesn't already exist.
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
  - GROUP BY modifies the entire query, like: `select customerId, count(*) as orderCount from Orders group by customerId`. GROUP BY normally reduces the number of rows returned by rolling them up and calculating averages or sums for each row.
  - But PARTITION BY just works on a window function, like ROW_NUMBER(): `select row_number() over (partition by customerId order by orderId) as OrderNumberForThisCustomer from Orders`. PARTITION BY does not affect the number of rows returned, but it changes how a window function's result is calculated.
  - [SQL Window Functions good reference 1 _vl](https://www.youtube.com/watch?v=Ww71knvhQ-s), [SQL Window Functions good reference 2 _vl](https://www.youtube.com/watch?v=KwEjkpFltjc), [Group by, Partition by difference](https://stackoverflow.com/questions/2404565/what-is-the-difference-between-partition-by-and-group-by)

```
Consider a table named TableA with the following values:
id  firstname                   lastname                    Mark
-------------------------------------------------------------------
1   arun                        prasanth                    40
2   ann                         antony                      45
3   sruthy                      abc                         41
6   new                         abc                         47
1   arun                        prasanth                    45
1   arun                        prasanth                    49
2   ann                         antony                      49

Example for Group By: select SUM(Mark)marksum,firstname from TableA group by id,firstName: 
Result:
marksum  firstname
----------------
94      ann                      
134     arun                     
47      new                      
41      sruthy   

Example for Partition By: SELECT SUM(Mark) OVER (PARTITION BY id) AS marksum, firstname FROM TableA
Result:
marksum firstname 
-------------------
134     arun                     
134     arun                     
134     arun                     
94      ann                      
94      ann                      
41      sruthy                   
47      new  
```

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

### SQL Questions: (From leetcode, open source repos, websites, etc.)

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
Note that if we do this: SELECT * FROM employee e1 INNER JOIN employee e2 ON e1.id = e2.managerId; then our output would be like (take it as reference, and then we can understand how above query worked): 
| e1.id | e1.name | e1.salary | e1.managerId | e2.id | e2.name | e2.salary | e2.managerId |
|-------|---------|-----------|--------------|-------|---------|-----------|---------------|
| 3     | Sam     | 60000     | NULL         | 1     | Joe     | 70000     | 3             |
| 4     | Max     | 90000     | NULL         | 2     | Henry   | 80000     | 4             |

Also, to explain with example how other joins would work for reference: 

Case 1: SELECT u.user_id, u.name, p.phone_number FROM users u LEFT JOIN phone_numbers p ON u.user_id = p.user_id;

Assume table 1: 

| user_id | name    |
|---------|---------|
| 1       | Alice   |
| 2       | Bob     |
| 3       | Charlie |
| 4       | David   |

And table 2: 

| user_id | phone_number |
|---------|--------------|
| 2       | 123-4567     |
| 3       | 987-6543     |

Result: 

| user_id | name    | phone_number |
|---------|---------|--------------|
| 1       | Alice   | NULL         |
| 2       | Bob     | 123-4567     |
| 3       | Charlie | 987-6543     |
| 4       | David   | NULL         |

Case 2: SELECT u.user_id, u.name, p.phone_number FROM users u LEFT JOIN phone_numbers p ON u.user_id = p.user_id;

Assume table 1: 

| user_id | name    |
|---------|---------|
| 1       | Alice   |
| 2       | Bob     |
| 3       | Charlie |
| 4       | David   |

And table 2: 

| user_id | phone_number |
|---------|--------------|
| 100       | 123-4567     |
| 101       | 987-6543     |

Result: 

| user_id | name    | phone_number |
|---------|---------|--------------|
| 1       | Alice   | NULL         |
| 2       | Bob     | NULL         |
| 3       | Charlie | NULL         |
| 4       | David   | NULL         |

Case 3: SELECT u.user_id, u.name AS user_name, p.name AS phone_name, p.phone_number FROM users u LEFT JOIN phone_numbers p ON u.user_id = p.user_id;

Assume table 1: 

| user_id | name    |
|---------|---------|
| 1       | Alice   |
| 2       | Bob     |
| 3       | Charlie |
| 4       | David   |

And table 2: 

| user_id | name    | phone_number |
|---------|---------|--------------|
| 2       | Robert  | 123-4567     |
| 3       | Charles | 987-6543     |

Result: 

| user_id | user_name | phone_name | phone_number |
|---------|-----------|------------|--------------|
| 1       | Alice     | NULL       | NULL         |
| 2       | Bob       | Robert     | 123-4567     |
| 3       | Charlie   | Charles    | 987-6543     |
| 4       | David     | NULL       | NULL         |

Also, another case to display a many-many join scenario: 

Assume table A: 

| id  | number |
|-----|--------|
| 1   | None   |
| 1   | None   |
| 1   | None   |

Assume table B: 

| id  | number |
|-----|--------|
| 1   | 93     |
| 1   | 93     |
| 1   | 93     |

It will lead to a 3*3 = 9 rows if we do a left join like: `SELECT * FROM A LEFT JOIN B ON A.id = B.id;`

| id  | A.number | id  | B.number |
|-----|----------|-----|----------|
| 1   | None     | 1   | 93       |
| 1   | None     | 1   | 93       |
| 1   | None     | 1   | 93       |
| 1   | None     | 1   | 93       |
| 1   | None     | 1   | 93       |
| 1   | None     | 1   | 93       |
| 1   | None     | 1   | 93       |
| 1   | None     | 1   | 93       |
| 1   | None     | 1   | 93       |

Even if we do inner join, result will be same. 

Write a solution to find the second highest salary from the Employee table. If there is no second highest salary, return null (return None in Pandas).
Input: 
Employee table:
+----+--------+
| id | salary |
+----+--------+
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |
+----+--------+
Output: 
+---------------------+
| SecondHighestSalary |
+---------------------+
| 200                 |
+---------------------+
SELECT MAX(Salary) AS SecondHighestSalary FROM Employee E2 WHERE E2.Salary < (SELECT MAX(Salary) FROM Employee)
or 
select (select distinct Salary from Employee order by salary desc limit 1 offset 1) as SecondHighestSalary; Note that SELECT DISTINCT(salary) from Employee order by salary DESC LIMIT 1 OFFSET N is the main logic here. 
or 
SELECT CASE WHEN COUNT(*) = 0 THEN NULL ELSE Salary END AS SecondHighestSalary
FROM (
  SELECT Salary, DENSE_RANK() OVER(ORDER BY Salary DESC) AS rnk
  FROM Employee
) as base 
WHERE rnk = 2

Write a solution to find all customers who never order anything.
Input: 
Customers table:
+----+-------+
| id | name  |
+----+-------+
| 1  | Joe   |
| 2  | Henry |
| 3  | Sam   |
| 4  | Max   |
+----+-------+
Orders table:
+----+------------+
| id | customerId |
+----+------------+
| 1  | 3          |
| 2  | 1          |
+----+------------+
Output: 
+-----------+
| Customers |
+-----------+
| Henry     |
| Max       |
+-----------+
SELECT name AS Customers FROM Customers WHERE Customers.id NOT IN (SELECT CustomerId FROM Orders); 
or
SELECT c.name AS Customers FROM Customers c LEFT JOIN Orders o ON c.id=o.customerId WHERE o.customerId IS NULL;

Write a solution to report all the duplicate emails. Note that it's guaranteed that the email field is not NULL.
Input: 
Person table:
+----+---------+
| id | email   |
+----+---------+
| 1  | a@b.com |
| 2  | c@d.com |
| 3  | a@b.com |
+----+---------+
Output: 
+---------+
| Email   |
+---------+
| a@b.com |
+---------+
select email as Email from Person group by email having count(email)>1
or
SELECT Email FROM (SELECT Email, COUNT(Email) AS CNT FROM Person GROUP BY Email) WHERE CNT > 1

Write a solution to find all dates' Id with higher temperatures compared to its previous dates (yesterday).
Input: 
Weather table:
+----+------------+-------------+
| id | recordDate | temperature |
+----+------------+-------------+
| 1  | 2015-01-01 | 10          |
| 2  | 2015-01-02 | 25          |
| 3  | 2015-01-03 | 20          |
| 4  | 2015-01-04 | 30          |
+----+------------+-------------+
Output: 
+----+
| id |
+----+
| 2  |
| 4  |
+----+
SELECT W1.id FROM Weather W1 JOIN Weather W2 ON W1.recordDate = DATE_ADD(W2.recordDate, INTERVAL 1 DAY) WHERE W1.temperature > W2.temperature;
or
SELECT id FROM Weather w1 WHERE temperature > (SELECT temperature FROM Weather w2 WHERE w2.recordDate = DATE_SUB(w1.recordDate, INTERVAL 1 DAY));







































----------------------------------------------------------------------

