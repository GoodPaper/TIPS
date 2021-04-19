# VI

#### 어떤 문자열을 다른 문자열로 전부다 바꾸고 싶다.
* %s/기존문자열(regex가능)/교체할문자열/g
  * %s: 문서 전체를 대상으로 문자열 바꾸겠다는 명령
  * g: 전체 적용, g 안쓰면 하나만 적용됨.
```bash
# Before
1.html
2.html
3.html

# :%s/html/json/g

# After
1.json
2.json
3.json
```

#### 정해진 범위의 줄을 주석 처리 하고 싶다.
* 시작라인수:종료라인s/^/#
  * bash shell이라서 주석 기호가 # 인 것이지, 다른 확장자 파일이면, 그에 맞는 기호를 넣으면 된다.
  * ^: beginning of the line
```bash
# Before
a
b
c

# :1,3s/^/#

# After
#a
#b
#c
```

#### Reference
* https://wiki.kldp.org/KoreanDoc/html/Vim_Guide-KLDP/Vim_Guide-KLDP.html
