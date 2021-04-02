# Order by

#### ASC, DESC
* ASC: Ascending, 오름 차순, 0, 1, 2 ....
* DESC: Descending, 내림 차순, 100, 99, 98 ...
```sql
# Basic
select * from what order by target_column;

# Alias
select a + b as bundle from what order by bundle;

# Order
select * from what order by 2;

# Multiple column
select * from what order by 3 asc, 1 desc;
```
* Reference
  * https://gomguard.tistory.com/93
  * https://docs.actian.com/ingres/10s/index.html#page/CharBasedQueryRep/Sort_Order_and_Data_Type.htm
