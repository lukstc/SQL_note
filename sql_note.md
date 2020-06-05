SQL delete and random delete
```SQL
## Simple DELETE
    DELETE [ TOP ( expression ) [ PERCENT ] ]  
    FROM table_name
    [WHERE search_condition];

## Random DELET to 10
    DELETE TOP 10 PERCENT FROM target_table;
```
