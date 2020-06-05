SQL case when syntax
```SQL
case
when ... then ...
when ... then ...
when ... then ...
else ...
# 'else' is optional, by default 'NULL'
end
;
```

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
```
```SQL
select salary,
  case
  when salary >= 80000 then'high'
  when salary >= 70000 then 'medium'
  else 'low'
end as 'level'
from employee
order by salary desc
;
```
```
salary	level
90000	high
85000	high
85000	high
80000	high
70000	medium
69000	low
60000	low
```
