## Problem

Write a SQL query to rank scores. 
If there is a tie between two scores, both should have the **same ranking**. <br/>
Note that after a tie, the next ranking number should be the next consecutive integer value. <br/>
In other words, there should be **no "holes" between ranks.**

```
+----+-------+
| Id | Score |
+----+-------+
| 1  | 3.50  |
| 2  | 3.65  |
| 3  | 4.00  |
| 4  | 3.85  |
| 5  | 4.00  |
| 6  | 3.65  |
+----+-------+
```

For example, given the above Scores table, your query should generate the following report (order by highest score):
```
+-------+------+
| Score | Rank |
+-------+------+
| 4.00  | 1    |
| 4.00  | 1    |
| 3.85  | 2    |
| 3.65  | 3    |
| 3.65  | 3    |
| 3.50  | 4    |
+-------+------+
```

## Analysis

For a score, its rank is the number of scores in the Scores table without duplicates that is **larger than or equal** to the score. <br/>
In above table, there are six scores, and four distinct scores: 3.50, 3.65, 3.85 and 4.00. <br/>
For 4.00, there is only one score 4.00 is greater than or equal to 4.00, so the rank of 4.00 is 1. <br/>
Similarly, for 3.65, there are three scores are greater than or equl to it: 4.00, 3.85, 3.65. So rank of 3.65 is 3.<br/>

First, get all distinct scores:
```
SELECT DISTINCT Score FROM Scores;
```
We call this distinct scores table **ranking**, <br/>
then we join ranking and Scores and filter scores in **ranking that is larger than or equal to each score in Scores**:

```
SELECT s.Score, ranking.Score FROM
(SELECT DISTINCT Score FROM Scores) AS ranking, Scores AS s
WHERE s.Score <= ranking.Score;
```
For each score in Scores, count how many scores in ranking are larger than or equal to it:
```
SELECT s.Score, COUNT(ranking.Score) AS Rank FROM
(SELECT DISTINCT Score FROM Scores) AS ranking, Scores AS s
WHERE s.Score <= ranking.Score
GROUP BY s.Id, s.Score;
```
Finally, sort by score in descending order:
```
SELECT s.Score, COUNT(ranking.Score) AS Rank FROM
(SELECT DISTINCT Score FROM Scores) AS ranking, Scores AS s
WHERE s.Score <= ranking.Score
GROUP BY s.Id, s.Score
ORDER BY s.Score DESC;
```

## Solution
```
SELECT s.Score as Score, COUNT(ranking.Score) AS Rank FROM
(SELECT DISTINCT Score FROM Scores) AS ranking, Scores AS s
WHERE s.Score <= ranking.Score
GROUP BY s.Id, s.Score
ORDER BY s.Score DESC;
```
