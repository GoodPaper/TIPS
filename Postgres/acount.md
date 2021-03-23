# Postgres 계정 관련

#### postgres 계정의 비밀 번호 설정( 초기 설정 )
```bash
# https://zetawiki.com/wiki/%EC%9A%B0%EB%B6%84%ED%88%AC_PostgreSQL_%EC%84%A4%EC%B9%98
# https://brunch.co.kr/@hjinu/3
$ sudo -u postgres psql
psql (9.5.12)
Type "help" for help.

postgres=# alter user postgres with password '비밀번호';
ALTER ROLE
postgres=# \q
$
```
#### 계정 추가
```bash
# https://zetawiki.com/wiki/PostgreSQL_%EA%B3%84%EC%A0%95_%EC%83%9D%EC%84%B1
# https://zetawiki.com/wiki/PostgreSQL_%EA%B3%84%EC%A0%95_%ED%8C%A8%EC%8A%A4%EC%9B%8C%EB%93%9C_%EC%A7%80%EC%A0%95
$ sudo -u postgres psql
psql (9.5.12)
Type "help" for help.

postgres=# \du
                                   List of roles
 Role name |                         Attributes                         | Member of
-----------+------------------------------------------------------------+-----------
 postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS | {}

postgres=# create role 계정;
CREATE ROLE
postgres=# \du
                                   List of roles
 Role name |                         Attributes                         | Member of
-----------+------------------------------------------------------------+-----------
 계정       | Cannot login                                               | {}
 postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS | {}

postgres=# alter role 계정 login password '비밀번호';
ALTER ROLE
postgres=# \du
                                   List of roles
 Role name |                         Attributes                         | Member of
-----------+------------------------------------------------------------+-----------
 계정       |                                                            | {}
 postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS | {}

postgres=#
```
#### 비밀번호 변경
```bash
$ sudo -u postgres psql
psql (9.5.12)
Type "help" for help.

postgres=# alter role 계정 with password '비밀번호';
ALTER ROLE
postgres=# \q
$
```
