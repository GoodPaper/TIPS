# SCP

#### 별도 port를 입력해야 하는 경우
```bash
# 문법: scp -P {포트번호} {보낼 파일이나 디렉토리} {받을 목적지 파일 혹은 디렉토리}
$ scp -P 9786 joker@1.2.3.6:/home/joker/material.json /home/ubuntu/material.v2.json
```

#### pem 파일을 이용하는 경우
```bash
# 문법: scp -i {pem 파일 경로} {보낼 파일이나 디렉토리} {받을 목적지 파일 혹은 디렉토리}
$ scp -i where/the/pem material.json ububtu@6.3.2.1:/home/ubuntu/material.v2.json
```
