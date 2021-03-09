# Volume 크기 확장

### 왜 알아보았는가?
* EC2 Instance에 SSH 접속이 불가능한 상황이 있었다. Status를 보니 Unreachable 하다고 나온다.
* AWS에 문의해 보니 Disk가 가용 공간이 모자르다고 나오는 문제가 있다고 한다.
* Linux( Ubuntu 18 )에서 Root volume의 가용공간이 모자르면 EC2 접속에 문제가 생긴다고 보면 된다.
* 본 글은 SSH로 해당 Instance에 접속이 가능하다는 전제하에 작성한다.
    * 접속이 불가능한 경우 접속 할 수 있는 또 다른 방법이 있다.

### 해결 방법
1. 물리적인 Volume 크기를 증가시킨다.
    * AWS Console 혹은 CLI 등...

2. 해당 Instance에 접속한다.

3. Terminal에서 **df** 명령어로 용량 현황을 확인한다. Swap 부분을 제외한 어느 부분에서 용량이 얼마나 사용하고 있는지가 나온다.
```bash
$ df -kh # df -ih
Filesystem      Size  Used Avail Use% Mounted on
...
/dev/xvda1      7.7G  7.7G  0G  100% /
...
# AWS EC2 에서 Root volume을 /dev/sda1으로 설정하면 내부에서는 /dev/xvda1로 잡히는 경우가 많다. 절대적인 것은 아니니 참고만...
```

4. **lsblk**로 파티션 현황을 확인한다.
```bash
$ lsblk
NAME    MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
xvda    202:0    0   8G   0 disk
└─xvda1 202:1    0   16G  0 part /
...
```

5. 파티션 확장을 위해서 임시 공간을 확보한다. 적어도 100M 정도?
    * /tmp나 /var/log 에서 필요 없는 파일들을 좀 제거해본다.

6. **growpart**로 파티션을 확장한다.
```bash
...
$ sudo growpart /dev/xvda 1 # Device와 Partition 번호에 공백 있는 것 주의
```

7. lsblk로 잘 늘어났는지 재 확인

8. **resize2fs**를 이용하여 파일 시스템 확장
```bash
$ sudo resize2fs /dev/xvda
...
```

9. **df** 명령어를 이용하여 재 확인. 용량이 늘어난 것이 확인된다.
```bash
$ df -kh # -ih
...
```

### 참조
* https://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/recognize-expanded-volume-linux.html
* https://aws.amazon.com/ko/premiumsupport/knowledge-center/ebs-volume-size-increase/
