```SQL
CREATE TABLE logs (
  `Id` INTEGER,
  `Num` INTEGER
);

INSERT INTO logs
  (`Id`, `Num`)
VALUES
  ('1', '1'),
  ('2', '1'),
  ('3', '1'),
  ('4', '2'),
  ('5', '1'),
  ('6', '2'),
  ('7', '2');
```
Write a SQL query to find all numbers that appear at least three times consecutively.
```
+----+-----+
| Id | Num |
+----+-----+
| 1  |  1  |
| 2  |  1  |
| 3  |  1  |
| 4  |  2  |
| 5  |  1  |
| 6  |  2  |
| 7  |  2  |
+----+-----+
```
For example, given the above Logs table, 1 is the only number that appears consecutively for at least three times.
```
+-----------------+
| ConsecutiveNums |
+-----------------+
| 1               |
+-----------------+
```
Solution
```SQL
# Write your MySQL query statement below
select distinct l2.num as 'ConsecutiveNums'
from logs as l1, logs as l2, logs as l3
where l1.id = l2.id-1
and l2.id+1 = l3.id
and l1.num = l2.num
and l2.num = l3.num
;
```
