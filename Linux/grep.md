# grep

### 언제 사용하는가?
어떤 결과로 나온 출력에서 원하는 글자나 패턴이 있는지 확인할 때 사용

#### 디렉토리 내 내가 원하는 파일이 어떻게 있나?
```bash
# json으로 끝나는 파일만 찾고자 함.
$ ls storage/ | grep '*.json'
```

#### 현재 디렉토리 기준으로 하위 파일들에서 특정 구문이 들어간 파일과, 그 내용을 보고 싶다.
```bash
# 현재 경로에 있는 파일들 내부에 Config라는 단어가 있으면, 그 단어가 포함된 문장을 출력해 준다.
$ grep -rnw * -e 'Config'
...
A.done:11:                "Config": 3,
D.done:12:                "Config": 2,
C.done:12:                "Config": 3,
D.done:12:                "Config": 2,
E.done:12:                "Config": 1,
...
```
