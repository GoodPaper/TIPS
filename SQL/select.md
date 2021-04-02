# SELECT

#### Alias로 Where 조건을 사용해 보고 싶다.
WHERE 절은 Select 문 처리 이전에 입력이 되기 때문에 Alias를 사용할 수 없다. 굳이 사용해야 겠다면, subquery를 사용한다.
```sql
SELECT *
FROM (
  SELECT A, B, C as THIS_IS_ALIAS FROM TABLE
) t
WHERE t.THIS_IS_ALIAS > 3;
```
* https://stackoverflow.com/questions/43790424/sql-is-it-possible-to-use-alias-in-where/43790534
