schema:
```SQL
CREATE TABLE teams (
  `team_id` INTEGER,
  `team_name` VARCHAR(11)
);

INSERT INTO teams
  (`team_id`, `team_name`)
VALUES
  ('10', 'Leetcode FC'),
  ('20', 'NewYork FC'),
  ('30', 'Atlanta FC'),
  ('40', 'Chicago FC'),
  ('50', 'Toronto FC');



CREATE TABLE matches (
  `match_id` INTEGER,
  `host_team` INTEGER,
  `guest_team` INTEGER,
  `host_goals` INTEGER,
  `guest_goals` INTEGER
);

INSERT INTO matches
  (`match_id`, `host_team`, `guest_team`, `host_goals`, `guest_goals`)
VALUES
  ('1', '10', '20', '3', '0'),
  ('2', '30', '10', '2', '2'),
  ('3', '10', '50', '5', '1'),
  ('4', '20', '30', '1', '0'),
  ('5', '50', '30', '1', '0');
  
```

Table: Teams
```
+---------------+----------+
| Column Name   | Type     |
+---------------+----------+
| team_id       | int      |
| team_name     | varchar  |
+---------------+----------+
```
team_id is the primary key of this table.
Each row of this table represents a single football team.
Table: Matches
```
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| match_id      | int     |
| host_team     | int     |
| guest_team    | int     |
| host_goals    | int     |
| guest_goals   | int     |
+---------------+---------+
```
match_id is the primary key of this table.
Each row is a record of a finished match between two different teams.
Teams host_team and guest_team are represented by their IDs in the teams table (team_id) and they scored host_goals and guest_goals goals respectively.


You would like to compute the scores of all teams after all matches. Points are awarded as follows:
A team receives three points if they win a match (Score strictly more goals than the opponent team).
A team receives one point if they draw a match (Same number of goals as the opponent team).
A team receives no points if they lose a match (Score less goals than the opponent team).
Write an SQL query that selects the team_id, team_name and num_points of each team in the tournament after all described matches. Result table should be ordered by num_points (decreasing order). In case of a tie, order the records by team_id (increasing order).

The query result format is in the following example:

Teams table:
```
+-----------+--------------+
| team_id   | team_name    |
+-----------+--------------+
| 10        | Leetcode FC  |
| 20        | NewYork FC   |
| 30        | Atlanta FC   |
| 40        | Chicago FC   |
| 50        | Toronto FC   |
+-----------+--------------+
```
Matches table:
```
+------------+--------------+---------------+-------------+--------------+
| match_id   | host_team    | guest_team    | host_goals  | guest_goals  |
+------------+--------------+---------------+-------------+--------------+
| 1          | 10           | 20            | 3           | 0            |
| 2          | 30           | 10            | 2           | 2            |
| 3          | 10           | 50            | 5           | 1            |
| 4          | 20           | 30            | 1           | 0            |
| 5          | 50           | 30            | 1           | 0            |
+------------+--------------+---------------+-------------+--------------+
```
Result table:
```
+------------+--------------+---------------+
| team_id    | team_name    | num_points    |
+------------+--------------+---------------+
| 10         | Leetcode FC  | 7             |
| 20         | NewYork FC   | 3             |
| 50         | Toronto FC   | 3             |
| 30         | Atlanta FC   | 1             |
| 40         | Chicago FC   | 0             |
+------------+--------------+---------------+
```

Solution:
```SQL
# Write your MySQL query statement below
select t1.team_id, t1.team_name, ifnull(sum(points),0) as num_points
from teams t1 left join (
    select host_team as team,
    case
    when host_goals > guest_goals then 3
    when host_goals = guest_goals then 1
    when host_goals < guest_goals then 0
    end as points
    from matches
    union all
    select guest_team as team,
    case
    when host_goals > guest_goals then 0
    when host_goals = guest_goals then 1
    when host_goals < guest_goals then 3
    end as points
    from matches
) as t2 on t1.team_id = t2.team
group by t1.team_id, t1.team_name
order by num_points desc, t1.team_id asc
;
```

Key Points:
- group by & sum: is sum => 0, the value will be NULL
  - could use 'ifnull' to fill
- union / union all
  - union: will remove duplicated ones
  - union all: will keep all the records
