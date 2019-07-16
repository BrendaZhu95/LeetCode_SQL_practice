## Problem

Mary is a teacher in a middle school and she has a table seat storing students' names and their corresponding seat ids. <br/>
The column id is continuous increment.<br/>
Mary wants to change seats for the adjacent students. <br/>
Can you write a SQL query to output the result for Mary?
```
+---------+---------+
|    id   | student |
+---------+---------+
|    1    | Abbot   |
|    2    | Doris   |
|    3    | Emerson |
|    4    | Green   |
|    5    | Jeames  |
+---------+---------+
```
For the sample input, the output is:
```
+---------+---------+
|    id   | student |
+---------+---------+
|    1    | Doris   |
|    2    | Abbot   |
|    3    | Green   |
|    4    | Emerson |
|    5    | Jeames  |
+---------+---------+
```
Note: <br/>
**If the number of students is odd, there is no need to change the last one's seat.**

## Analysis

We need to use IF() to concider different situations. <br/>
If the total number of students is odd, then we only need to keep the last id as same as before.<br/>
For the rest of the students, we need to change adjacent ids. <br/>
If the student id is odd, we need to change it to next even id. For example, change 1 to 2. <br/>
Similarlay, if the student id is even, we need to change it to last odd id. For example, change 2 to 1.<br/>

## Solution
```
SELECT IF((SELECT COUNT(id) FROM seat)%2 = 1 AND id = (SELECT COUNT(id) FROM seat), id, 
IF(id % 2 =1, id+1, id-1)) AS id, student
FROM seat 
ORDER BY id
```
