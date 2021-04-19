# VPN  

#### How setup?
##### 0. Prerequisite
* VPC가 이미 설정되어 있어야 한다. Region 별 Default를 사용하건, 개별적인 VPC를 만들어서 사용하건, 만들어 놓아야 한다.
##### 1. Customer gateway
* VPC → VPN Connection → Customer Gateways로 이동
* Customer gateway를 새로 만든다. (Create Customer Gateway 클릭)
* Name 기재 → Routing은 static으로 지정 → IP Address는 Vendor사에서 제공한다. 그 주소를 기재한다.
##### 2. Virtual Private Gateways
* VPC → VPN Connection → Virtual Private Gateways로 이동
* Create Virtual Private Gateway 클릭
* Name 기재 → 새로운 Virtual gateway가 생긴것 확인 → status가 <span style="color:red">detached</span>라고 되어 있는 것을 확인한다.
* Table에서 새로 생긴 Virtual gateway 마우스 오른쪽 클릭 → context menu에서 Attach to VPC 클릭 → 원하는 VPC에 붙인다.
* state가 <span style="color:green">attached</span>라고 초록색으로 변경된 것을 확인한다.
* VPC 내 VPN을 구성하고자 하는 Subnet을 담당하는 Route table로 이동한다. Route table을 하나 클릭하면 Route propagation이 있는데, 여기에 Virtual private gateway가 보일 것이다.
  * Edit을 눌러서 propagate를 누르고 Save를 한다. 그럼 이 Route를 통해서 VPN Tunnel이 형성될 수 있게 된다.
##### 3. VPN Connections
* VPC → VPN Connection → VPN Connections로 이동
* Create VPN Connection 클릭
  * Name 기재
  * Virtual Private Gateway는 우리가 방금 만들었던 것으로 선택
  * Customer Gateway는 Existing으로 선택하고, 우리가 이전에 만들었던 Customer gateway 선택
  * Routing option은 Static으로 선택
    * Vendor사에서 받은 Inside IP CIDR을 기재한다. ( N개 받았으면, N개 다 넣으면 됨. UP, DOWN Backup 용임. )
  * Tunnel Option에는 우리가 사용할 Inside IP CIDR을 기재한다. 암호는 Vendor 사에서 요청한 것을 사용한다.
    * AWS에서 제공하는 Inside CIDR은 현재 기준으로 ?.?.?.?/16 범위내에서 /30 주소로 만들 수 있다.
* State가 available 이라고 변하면 Tunnel이 준비가 된 것이다.
* AWS Managed VPN은 우리가 만든 VPN의 설정 정보를 파일로 만들어 준다. 필요시 이를 다운로드 하여, 업체에 공유해주면, Tunnel을 UP할 때 도움이 된다.
  * Vendor, Platform, Software를 선택할 수 있음.  
* Tunnel details 탭에 들어가면 2개의 Tunnel과 그 상태 정보가 나와있는 것을 확인할 수 있다. 현재는 모두 DOWN 일 것이다.
* Tunnel이 UP이 되려면, 상대방 쪽에서 Tunneling 시도를 해서 성공되어야 한다. 이를 상대방에게 알려준다.
  * UP이 잘 되면 상대방한테도 연결 잘 되었다고 알려줄 것. ( 관례상... )
##### 4. Tunneling
* 여기서부터의 내용은 상대방 측과 VPN을 연결하기 위한 상세 내용이 전개된다. 본 Section의 정보는 상대방과 Connection을 어떻게 맺을 것이냐에 따라서 달라진다.
* 우리가 만든 VPN에 가서 Tunnel details를 확인해 보면, 우리 측 Tunnel의 외부 IP - 내부 IP/CIDR 쌍이 2개 있는 것을 확인 할 수 있다. (1개는 Backup용으로 AWS에서 제공하는 것이다.)
* Vendor와 IP 정보를 일정 부분 공유 해야 한다. 그래야 연결이 이루어 질 수 있으니... 그런데 정보를 알려준 이후에도 UP이 되지 않는 경우가 있다. 이는 이유가 각각이지만, 나의 경우는 아래와 같이 해봤다.
  * Tunnel이 UP이 안된다. Vendor에 얘기도 해봤고, ping, nmap 다 해봤는데 연결이 안된다. → AWS에서 말하길 Vendor의 VPN 쪽에 no-nat-traversal을 Configure 하라고 조언하였다. → 이거 하고 Tunnel이 UP이 되었다.
* Tunnel로 왔다 갔다(In and out)한 메트릭 정보를 확인하고 싶다면 Cloudwatch를 확인하면 된다.

##### 5. Use VPN ( ICE Dependency )
* 이 다음 단계는 Vendor와의 관계이므로, 알아서 잘 대응하면 된다.

#### Reference
* 작업 시점: September 2019
* https://youtu.be/3j1MLlgc5Eg
