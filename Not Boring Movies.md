## Problem

X city opened a new cinema, many people would like to go to this cinema. <br/>
The cinema also gives out a poster indicating the movies’ ratings and descriptions.<br/>
Please write a SQL query to output movies with **an odd numbered ID** <br/>
and a description that **is not 'boring'**. **Order the result by rating.** <br/>

For example, table cinema:
```
+---------+-----------+--------------+-----------+
|   id    | movie     |  description |  rating   |
+---------+-----------+--------------+-----------+
|   1     | War       |   great 3D   |   8.9     |
|   2     | Science   |   fiction    |   8.5     |
|   3     | irish     |   boring     |   6.2     |
|   4     | Ice song  |   Fantacy    |   8.6     |
|   5     | House card|   Interesting|   9.1     |
+---------+-----------+--------------+-----------+
```
For the example above, the output should be:
```
+---------+-----------+--------------+-----------+
|   id    | movie     |  description |  rating   |
+---------+-----------+--------------+-----------+
|   5     | House card|   Interesting|   9.1     |
|   1     | War       |   great 3D   |   8.9     |
+---------+-----------+--------------+-----------+
```
## Analysis

If we want to select odd id from the table, we need to use MOD() function <br/>

SQL MOD() function is used to get the remainder from a division. <br/>
The SQL DISTINCT command along with the SQL MOD() function is used to retrieve only unique records 
depending on the specified column or expression. <br/>

Syntax:<br/>
MOD( dividend, divider )<br/>

## Solution
```
SELECT id, movie, description, rating FROM cinema
WHERE description NOT LIKE '%boring%'
AND MOD(id, 2) = 1
ORDER BY rating DESC
```
