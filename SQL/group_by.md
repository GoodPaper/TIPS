# Group by

#### 기본 사용법
```sql
-- target column으로 묶어서 보는 경우
SELECT target, COUNT( col2 ) AS cnt FROM table GROUP BY target;
```

#### 그룹 중 특정 아이템의 개수가 특정 범위에 들어있는 경우, Having
```sql
-- 2개 이상인 것만 보겠다.
SELECT target, COUNT( col2 ) AS cnt FROM table GROUP BY target HAVING cnt > 1;
```

#### 1개 이상의 Column에 대해서 Group by를 하고자 하는 경우
보통 Group by를 사용할 때는 1개 Column 만 사용하는 경우가 많다. 2개 이상을 선택하는 경우, 각 Column의 Distinct 에서 Combination을 만든다고 보면 된다. 경우의 수를 모두 만든다고 생각하면 됨.
```sql
--
--+---------+----------+----------+
--| Code    | Interval | Who      |
--+---------+----------+----------+
--| KIT101  |        1 | John     |
--| KIT101  |        1 | Bob      |
--| KIT101  |        1 | Mickey   |
--| KIT101  |        2 | Jenny    |
--| KIT101  |        2 | James    |
--| COV119  |        1 | John     |
--| COV119  |        1 | Erica    |
--+---------+----------+----------+

SELECT A, B, COUNT( * ) FROM table GROUP BY A, B;
SELECT A, B, COUNT( * ) FROM table GROUP BY B, A; -- Group by 에서 A, B 바꾼다고 달라지는 것은 없다.

--+---------+----------+-------+
--| Code    | Interval | Count |
--+---------+----------+-------+
--| KIT101  |        1 |     3 |
--| KIT101  |        2 |     2 |
--| COV119  |        1 |     2 |
--+---------+----------+-------+

```

#### Reference
* https://extbrain.tistory.com/56
* https://stackoverflow.com/questions/2421388/using-group-by-on-multiple-columns
