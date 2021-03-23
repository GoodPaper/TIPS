# Constraints

#### Synopsis
> SET CONSTRAINTS { ALL | name [, ...] } { DEFERRED | IMMEDIATE }

SET CONSTRAINTS sets the behavior of constraint checking within the current transaction. IMMEDIATE constraints are checked at the end of each statement. DEFERRED constraints are not checked until transaction commit. Each constraint has its own IMMEDIATE or DEFERRED mode.

SET CONSTRAINTS는 현재 수행중인 Transaction에 특정 Constraint를 적용할 때 사용된다. IMMEDIATE Constraint는 매 Statement 끝에서 Check된다. DEFFERED Constraint는 Transaction이 Commit 되기 전까지는 Check되지 않는다.

```
SET CONSTRAINTS ALL DEFFERED
SET CONSTRAINTS ALL IMMEDIATE
```
* https://www.postgresql.org/docs/9.1/static/sql-set-constraints.html
