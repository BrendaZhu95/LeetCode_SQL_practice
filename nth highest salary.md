## Problem

Write a SQL query to get the nth highest salary from the **Employee** table.
```
+----+--------+
| Id | Salary |
+----+--------+
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |
+----+--------+
```
For example, given the above Employee table, the nth highest salary where n = 2 is 200. 
If there is no nth highest salary, then the query should return null.
```
+------------------------+
| getNthHighestSalary(2) |
+------------------------+
| 200                    |
+------------------------+
```
## Analysis
Use **LIMIT** and **OFFSET**.
Sort by salary in descending order, then **skip n-1 numbers** and **output the first number.**

>Introduction to SQL LIMIT OFFSET clause
>To retrieve a portion of rows returned by a query, you use the LIMIT and OFFSET clauses. 
>The OFFSET clause **skips the offset rows** before beginning to return the rows. 
>If you use both LIMIT and OFFSET clauses the OFFSET **skips offset rows first before the LIMIT constrains the number of rows**.

## Solution
```
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
  SET N=N-1;
  RETURN (
      # Write your MySQL query statement below.
      SELECT DISTINCT Salary FROM Employee ORDER BY Salary DESC LIMIT 1 OFFSET N
  );
END
```
