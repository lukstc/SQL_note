```SQL
CREATE TABLE employee (
  `Id` INTEGER,
  `Name` VARCHAR(5),
  `Salary` INTEGER,
  `DepartmentId` INTEGER
);

INSERT INTO employee
  (`Id`, `Name`, `Salary`, `DepartmentId`)
VALUES
  ('1', 'Joe', '85000', '1'),
  ('2', 'Henry', '80000', '2'),
  ('3', 'Sam', '60000', '2'),
  ('4', 'Max', '90000', '1'),
  ('5', 'Janet', '69000', '1'),
  ('6', 'Randy', '85000', '1'),
  ('7', 'Will', '70000', '1');

CREATE TABLE department (
  `Id` INTEGER,
  `Name` VARCHAR(5)
);

INSERT INTO department
  (`Id`, `Name`)
VALUES
  ('1', 'IT'),
  ('2', 'Sales');
```
The Employee table holds all employees. Every employee has an Id, and there is also a column for the department Id.
```
+----+-------+--------+--------------+
| Id | Name  | Salary | DepartmentId |
+----+-------+--------+--------------+
| 1  | Joe   | 85000  | 1            |
| 2  | Henry | 80000  | 2            |
| 3  | Sam   | 60000  | 2            |
| 4  | Max   | 90000  | 1            |
| 5  | Janet | 69000  | 1            |
| 6  | Randy | 85000  | 1            |
| 7  | Will  | 70000  | 1            |
+----+-------+--------+--------------+
```
The Department table holds all departments of the company.
```
+----+----------+
| Id | Name     |
+----+----------+
| 1  | IT       |
| 2  | Sales    |
+----+----------+
```
Write a SQL query to find employees who earn the top three salaries in each of the department. For the above tables, your SQL query should return the following rows (order of rows does not matter).
```
+------------+----------+--------+
| Department | Employee | Salary |
+------------+----------+--------+
| IT         | Max      | 90000  |
| IT         | Randy    | 85000  |
| IT         | Joe      | 85000  |
| IT         | Will     | 70000  |
| Sales      | Henry    | 80000  |
| Sales      | Sam      | 60000  |
+------------+----------+--------+
```
Explanation:

In IT department, Max earns the highest salary, both Randy and Joe earn the second highest salary, and Will earns the third highest salary. There are only two employees in the Sales department, Henry earns the highest salary while Sam earns the second highest salary.

solution-1
```SQL
# Write your MySQL query statement below
select e1.name as 'Name', e1.salary 'Salary', d.name as 'Department'
from employee e1 inner join department as d on e1.departmentid = d.id
where 3 > (
  select count(distinct e2.salary)
  from employee e2
  where e1.departmentid = e2.departmentid and e1.salary < e2.salary
  )
order by e1.salary desc
;
```

solution-2
```SQL
select d.name as Department, t.name as 'Employee', t.salary as 'Salary'
from department as d, (
  select salary, name, departmentid,
  dense_rank() over(partition by departmentid order by salary desc) as 'dense_rank'
  from employee
) as t
where t.departmentid = d.id and t.dense_rank <= 3
;
```
