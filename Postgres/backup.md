# Backup

#### 왜 했었나?
ubuntu 16 에서 18로 업그레이드를 하는데, postgresql의 default version도 9.5에서 10.6으로 업그레이드 되었다. 데이터를 정상적으로 backup 하여 restore 하는 과정을 진행했다.

#### 진행 과정, pg_dump & pg_restore
```bash
# 참고: 본 작업은 PG 9.5에서 데이터를 덤프해서 PG 10.6에 집어 넣은 작업에 대한 내용이다.
# 1. 먼저 데이터를 가지고 있는 인스턴스에 접속한다.
# 2. 아래 명령어를 입력한다. ( http://postgresql.kr/docs/9.5/app-pgdump.html )
$ pg_dump -U 사용자 -d DB이름 --data-only --format=t --file=파일명.tar
...

# 3. Backup할 DB에는 이미 스키마가 설정되어 있어야 한다. ( 테이블이나, 인덱스 등 DDL에 해당되는 구문이 이미 실행되어 있어야 한다는 의미. ) 아직 준비되지 않았다면, 이 단계에서라도 만들어 놓아라.
# 4. 덤프한 데이터를 새로 만든 DB에 밀어 넣는다. ( https://www.postgresql.org/docs/10/app-pgrestore.html )

# 5. 데이터를 확인해서 정상적으로 다 들어갔는지 확인한다.
$: pg_restore -U 사용자 -d DB이름 --data-only 파일명.tar
...
```

#### 의견
원칙적으로는 DB의 Command로 backup 하고, restore 하는 것도 좋지만, 애초에 Flat 한 데이터가 있고, 이를 담을 수 있는 Scheme가 있다면, Flat 한 데이터를 주기적으로 Backup 해 놓고, 처음에 DB에 그 Scheme를 만들어서 집어 넣으면 문제될 것이 없다. 물리적으로 DBMS의 Version이건 다른 문제이건, 여기에 종속적이지 않게 됨.
