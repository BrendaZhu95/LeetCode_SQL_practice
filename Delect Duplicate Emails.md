## Problem

Write a SQL query to delete all duplicate email entries in a table named Person, 
keeping only unique emails based on its **smallest Id**.
```
+----+------------------+
| Id | Email            |
+----+------------------+
| 1  | john@example.com |
| 2  | bob@example.com  |
| 3  | john@example.com |
+----+------------------+
```
Id is the primary key column for this table.<br/>

For example, after running your query, the above Person table should have the following rows:
```
+----+------------------+
| Id | Email            |
+----+------------------+
| 1  | john@example.com |
| 2  | bob@example.com  |
+----+------------------+
```
Note:<br/>

Your output is the whole Person table after executing your sql. **Use delete statement.**

## Analysis
DELETE Syntax<br/>
DELETE FROM table_name WHERE condition;

When I tried query
```
DELETE FROM Person WHERE Id NOT IN
(SELECT * FROM (SELECT min(Id) FROM Person group by Email))
```
An error happened
```
You can't specify target table for update in FROM clause
```
The reason is I tried to update this table after I selected some information from the original table. <br/>
The solution is I should give a new name for selected table, then update this new table.

## Solution
```
DELETE FROM Person WHERE Id NOT IN
(SELECT * FROM (SELECT min(Id) FROM Person group by Email) as p)
```
