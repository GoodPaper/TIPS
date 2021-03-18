# tar 사용법

#### /bin/tar: Argument list too long
```
# 별도의 파일에 압축해야할 목록을 기재해 놓고, 이를 읽어 압축을 시도하면 된다.
# https://major.io/2007/07/05/bintar-argument-list-too-long/
# https://unix.stackexchange.com/questions/38955/argument-list-too-long-for-ls
$ find . name '*.json' -printf '%f\n' > /tmp/OOO.txt
$ tar -cjf something.tar.bz2 --files-from /tmp/OOO.txt
$ rm -i /tmp/OOO.txt
```

#### tar.bz2로 만들고 싶다면?
```bash
# Pack
$ tar cjf 압축파일이름.tar.bz2 대상들

# Unpack
$ tar xf 압축파일이름.tar.bz2
```
