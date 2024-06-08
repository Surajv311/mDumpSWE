
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
- Window/ Analytic Functions in sql: ORDER BY, PARTITION BY, RANK(), DENSE_RANK(), ROW_NUMBER(), LEAD(), LAG(). [Window functions sql example _vl](https://www.youtube.com/watch?v=Ww71knvhQ-s&ab_channel=techTFQ) Eg: 

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


----------------------------------------------------------------------





















