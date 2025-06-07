# Sql2

Problem 1 : Rank Scores		(https://leetcode.com/problems/rank-scores/ )


Problem 2 : Exchange Seats	(https://leetcode.com/problems/exchange-seats/ )

Problem 3 : Tree Node		(https://leetcode.com/problems/tree-node/ )

Problem 4 : Deparment Top 3 Salaries		(https://leetcode.com/problems/department-top-three-salaries/ )


Problem 1 : Rank Scores		(https://leetcode.com/problems/rank-scores/ )

SELECT 
    score,
    DENSE_RANK() OVER (ORDER BY score DESC) AS 'rank'
FROM 
    Scores;


Problem 2 : Exchange Seats	(https://leetcode.com/problems/exchange-seats/ )

SELECT 
    CASE
        WHEN id % 2 = 1 AND id + 1 <= (SELECT MAX(id) FROM Seat) THEN id + 1
        WHEN id % 2 = 0 THEN id - 1
        ELSE id
    END AS id,
    student
FROM Seat
ORDER BY id;


Problem 3 : Tree Node		(https://leetcode.com/problems/tree-node/ )

SELECT 
    t1.id,
    CASE 
        WHEN t1.p_id IS NULL THEN 'Root'
        WHEN t1.id IN (SELECT DISTINCT p_id FROM Tree WHERE p_id IS NOT NULL) THEN 'Inner'
        ELSE 'Leaf'
    END AS type
FROM Tree t1;



Problem 4 : Deparment Top 3 Salaries		(https://leetcode.com/problems/department-top-three-salaries/ )

SELECT 
    d.name AS Department,
    e.name AS Employee,
    e.salary AS Salary
FROM (
    SELECT *,
           DENSE_RANK() OVER (PARTITION BY departmentId ORDER BY salary DESC) AS rnk
    FROM Employee
) e
JOIN Department d ON e.departmentId = d.id
WHERE rnk <= 3;

