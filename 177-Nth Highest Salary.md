Write a SQL query to get the nth highest salary from the Employee table.
```
+----+--------+
| Id | Salary |
+----+--------+
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |
+----+--------+
```

For example, given the above Employee table, the nth highest salary where n = 2 is 200. If there is no nth highest salary, then the query should return null.

```
+------------------------+
| getNthHighestSalary(2) |
+------------------------+
| 200                    |
+------------------------+
```

```SQL
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
  RETURN (
      # Write your MySQL query statement below.
      SELECT salary
      FROM Employee e1
      WHERE N-1 = (
          SELECT COUNT(DISTINCT salary)
          FROM Employee e2
          WHERE e2.salary > e1.salary
      )
  );
END
```

```SQL
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
RETURN (
# Write your MySQL query statement below.
    select distinct salary from (
        select salary, dense_rank() over(order by salary desc) as ranks
        from employee
    ) as t1
    where ranks = N
);
END
```
