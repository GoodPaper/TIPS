# Linux Cron 문법

```bash
# 분(0-59) 시(0-23) 일(1-31) 월(1-12) 요일(0(일)-6(토)) 명령어
  * * * * * command
```

###예제
* 매 1분 마다 수행
```bash
* * * * * what_u_want_to_do
```
* 매 15, 45분에 수행
```bash
15,45 * * * * what_u_want_to_do
```
* 2분마다 수행
```bash
*/2 * * * * what_u_want_to_do
```
* 매일 2시 수행
```bash
0 2 * * * what_u_want_to_do
```
* 평일 8시마다 수행
```bash
0 8 * * 1-5 what_u_want_to_do
```
* 주말 8시마다 수행
```bash
0 8 * * 0,6 what_u_want_to_do
```

###기타 옵션
* 등록된 Cron script 확인
```bash
crontab -l
```

* Cron Script 직접 수정
```bash
crontab -e
```

* 수정된 내용 새로 반영
```bash
sudo systemctl restart cron.service
```


###기타
* User 별로 cron은 다르게 동작한다. sudo 사용시 확인.
* 특정 환경 변수를 입력하고 싶다면, cron script 상단에 원하는 설정을 입력한다. 예를 들어, DBLOCATION을 SSH로 설정하고 싶다면
```bash
...
DBLOCATION=SSH
...
cron scripts...
...
```

### 참조
* https://zetawiki.com/wiki/%EB%A6%AC%EB%88%85%EC%8A%A4_%EB%B0%98%EB%B3%B5_%EC%98%88%EC%95%BD%EC%9E%91%EC%97%85_cron,_crond,_crontab
