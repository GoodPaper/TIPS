# apt

### 명령어 정리
|Command|Description|
|--|--|
|agt-get update|사용 가능한 패키지 목록과 그것들의 버전을 업데이트 한다. 사용 가능한 목록을 업데이트 하는 것이지, 이를 실제로 설치(Install) 혹은 업그레이드(Upgrade) 하는 것이 아님.|
|agt-get upgrade|입력 받은 패키지를 업그레이드 한다. 위의 update를 먼저 실행하면, upgrade를 수행할 때, 버전 업그레이드 가능한 패키지와 그 버전 정보를 나열해 준다. 그래서 보통 update를 먼저 하고, upgrade를 수행한다.<br/><br/> upgrade is used to install the newest versions of all packages currently installed on the system from the sources enumerated in /etc/apt/sources.list. Packages currently installed with new versions available are retrieved and upgraded; under no circumstances are currently installed packages removed, or packages not already installed retrieved and installed. New versions of currently installed packages that cannot be upgraded without changing the install status of another package will be left at their current version. An update must be performed first so that apt-get knows that new versions of packages are available. |
|agt-get dist-upgrade|dist-upgrade in addition to performing the function of upgrade, also intelligently handles changing dependencies with new versions of packages; apt-get has a "smart" conflict resolution system, and it will attempt to upgrade the most important packages at the expense of less important ones if necessary. The dist-upgrade command may therefore remove some packages. The /etc/apt/sources.list file contains a list of locations from which to retrieve desired package files. See also apt_preferences(5) for a mechanism for overriding the general settings for individual packages.|
|apt-cache show {package}|패키지 상세 정보 출력|

* Reference
  * https://askubuntu.com/questions/94102/what-is-the-difference-between-apt-get-update-and-upgrade
  * https://unix.stackexchange.com/questions/361814/whats-the-difference-between-software-update-and-upgrade
  * http://taewan.kim/tip/apt-apt-get/
