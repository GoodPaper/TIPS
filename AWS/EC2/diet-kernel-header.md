# Diet old kernel

### 왜 알아보았는가?
* EC2 용량이 부족해서 어느 부분이 큰 공간을 차지하는지 확인해 보았다.
* /usr/src에 linux-headers-... 이런 Directory들이 점점 쌓이는 것을 확인하였다.

### 저 파일들은 무엇인가? 지워도 되는가?
* /usr/src 에는 프로그램 설치에 필요한 Source 파일들이 저장된다.
* 무턱대고 지울 수는 없겠다.
* linux-header-... 파일들이 대상인데, 확인 결과 지울수 있다고 한다.

### 어떻게 삭제하는가?
```bash
$ sudo apt-get autoremove --purge # 경우에 따라 -f 옵션 추가.
...
```

### 참조
* https://askubuntu.com/questions/253048/safe-to-remove-usr-src-linux-headers-after-purging-older-linux-images
* https://tesilio.github.io/ubuntu-low-free-space
* https://codechacha.com/ko/linux-apt-purge-vs-remove/
* https://webdir.tistory.com/101
