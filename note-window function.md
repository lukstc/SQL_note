For test: [MySQL Playground](https://www.db-fiddle.com/)
Reference:
- MySQL: [MySQL 8.0 Reference Manual](https://dev.mysql.com/doc/refman/8.0/en/window-function-descriptions.html)
- Tutorial:
  - [通俗易懂的学会：SQL窗口函数](https://zhuanlan.zhihu.com/p/92654574)
  - [精益SQL —— “窗口函数”的正确食用方式](https://zhuanlan.zhihu.com/p/60226935)

```SQL
CREATE TABLE employee (
  `Id` INTEGER,M
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

select *, rank() over(partition by departmentid order by salary desc) as ranking
from employee
;
```

排序窗口函数
```SQL
rank()
dense_rank()
row_number()
```

聚合窗口函数
```SQL
SUM(sale_price)over(partition by 日期 order by 时间) as date_sum

SUM(sale_price) over(order by product_id rows 1 preceding)

SUM(sale_price) over(order by product_id rows 1 following)

SUM(sale_price) over(order by product_id rows between 1 preceding and 2 following) 
```
