# Windows

#### 특정 Port를 Inbound( 들어오는 ) 방향으로 열고자 한다.
1. Windows Defender Firewall에 들어간다. ( 검색 -> 'Firewall' 입력해서 들어감. )
2. 고급 설정에서 Inbound Rule을 선택한다. 마우스 오른쪽 클릭으로 새 규칙을 만든다. 여기서 Port 지정하고 오픈하면 된다.
  * https://wiki.mcneel.com/ko/zoo/window7firewall
3. 설정 적용 후 같은 네트워크에 있는 PC에서 이번에 지정한 Port로 접근 가능한지 Test 해 본다.

#### 주기적인 작업을 등록하고자 하는 경우
리눅스 cron과 동일한 설정을 윈도우에서 하고 싶다면 Task scheduler를 이용한다. ( 검색 -> 'Task'... )
  * PC 재부팅 작업, 특정 어플리케이션을 언제 실행할 지 지정할 수 있다.
  * 권한에 대해서 잘 확인할 것.

#### Linux에서 Bash를 실행하는 것 처럼 특정 스크립트를 윈도우에서 실행하고 싶다면?
* Linux에서 스크립트 확장자를 sh로 붙인다면, 윈도우에서는 bat을 붙인다. bat 파일 안에는 window cmd 상에서 구동될 수 있는 명령을 기재한다.
* 디테일한 문법에 대해서는 검색 해 보아야 함.
```batch
@echo off
/path/of/binary /path/of/script.py *args %*
pause
```

#### Linux의 tail과 같은 명령어를 사용하고 싶다. ( Trace log )
* powershell -> Get-Content 명령어를 이용한다.
    - https://yuien.tistory.com/entry/Windows-%EC%9C%88%EB%8F%84%EC%9A%B0%EC%97%90%EC%84%9C-Tail-%EB%AA%85%EB%A0%B9%EC%96%B4-%EC%82%AC%EC%9A%A9-%EB%B0%A9%EB%B2%95
```batch
# Wait은 -f 옵션과 동일하게 following 수행.
$ Get-Content {path} -Wait
```
