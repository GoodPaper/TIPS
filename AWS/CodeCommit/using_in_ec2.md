# EC2에서 Code commit 사용하는 방법

### A. Role 생성
* Role를 하나 만든다. 본 Role의 목적은 EC2 Instance에서 CodeCommit을 사용하기 위함이다.
* Policy 중 AWSCodeCommitPowerUser를 선택 및 추가한다.
  * 정확하게는 CodeCommit:GitPull, CodeCommit:GitPush를 사용하기 위함인데, 해당 정책에는 이런 것이 모두 포함되어 있다.
  
### B. Repository 생성
* Code commit에서 Repository를 생성한다.
  
### C. EC2 - 외부 설정
1. EC2를 새로 생성하거나, 기존 개발 용도로 사용하고 있는 Instance를 하나 지정한다.
2. 지정한 EC2 Instance의 Role를 A과정에서 생성한 Role로 연결한다.
  
### D. EC2 - 내부 설정
1. python, awscli를 설치한다.
```bash
$ sudo apt-get install -y python3 python3-devel awscli
```
2. aws 환경 설정을 진행한다.
```bash
$ aws configuration
AWS Access Key ID []: ~~~
AWS Secret Access Key []: ~~~
Default region name [None]: ~~~
Default output format [None]: ~~~
```
3. git-remote-codecommit 이라는 python package를 설치한다.
```bash
$ sudo pip3 install git-remote-codecommit
```
  * 주의: sudo로 해야한다. git-remote-codecommit을 설치하면, 설치 마지막에 환경변수 설정하는 과정이 있는데, sudo를 사용하지 않으면, 설정이 완료되지 않고, Warning이 나온다. 물론 환경 변수 Setup 작업을 별도로 수행한다고 하면 sudo를 사용하지 않아도 된다.
  
### E. CodeCommit 사용
1. EC2내 원하는 경로로 이동한다.
2. 아래 명령어로 Repository를 복제한다.
  * 해당 주소는 HTTPS(GRC) 복제의 주소이다.
```bash
# region: 지역 코드
# respository: repository 이름
$ git clone codecommit::{region}://{repository}
```
  
# Reference
* https://docs.aws.amazon.com/codecommit/latest/userguide/setting-up-git-remote-codecommit.html?icmpid=docs_acc_console_connect