# Journal

### 왜 알아보았는가?
* 용량이 모자라서 확인해 보았더니, /var/log/journal이 큰 부분을 차지하고 있었다.
* 시스템 운영에 반드시 필요한 부분인지 확인. ( 아니면, 데이터를 줄여서 용량 확보 )

### Journal이 무엇인가?
* systemd의 로그. 바이너리 형태로 저장한다.
* 보통 journalctl을 이용한다.


###예제

1. 로그 확인
```bash
$ sudo journalctl # 로그 확인
$ sudo journalctl -n 10 # 최근 10 줄만 확인
$ sudo journalctl -x # 상세 설명 추가
$ sudo journalctl -f # tail -f 처럼 계속 Streaming 해서 출력하도록 하기
$ sudo journalctl -n _PID=123 # 특정 PID만 보기
$ sudo journalctl --since 2021-01-03 # 특정 일자 이후의 로그만 보기
```

2. 로그 삭제
```bash
$ sudo journalctl --vacuum-time=2d # 2일 이상된 내용 전부 삭제
...
Vacuuming done, freed 4.0G of archived journals on disk.


$ sudo journalctl --vacum-size=2G # 2G만 남기고 전부 삭제
...
Vacuuming done, freed 1.0G of archived journals on disk.
```
### 참조 TODO
* https://ma.ttias.be/clear-systemd-journal/
* https://github.com/tldr-pages/tldr/blob/master/pages/linux/journalctl.md
* https://www.lesstif.com/system-admin/linux-journalctl-82215080.html
