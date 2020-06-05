SQL delete and random delete
```SQL
## Simple DELETE
    DELETE [ TOP ( expression ) [ PERCENT ] ]  
    FROM table_name
    [WHERE search_condition];

## Random DELET to 10
    DELETE TOP 10 PERCENT FROM target_table;
```

Drop / Truncate TABLE
```SQL
# if exists [optional]
DROP TABLE if exists Shippers;

# The TRUNCATE TABLE command deletes the data inside a table, but not the table itself.
TRUNCATE TABLE Categories;
```


rank & row number
```SQL
set @row := 0;
select *, (@row := @row + 1) row_number
from employee
order by 1;
```
