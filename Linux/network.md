# Network

#### Ubuntu 고정 IP 설정
1. ifconfig 로 유선으로 연결된 Network device의 이름을 알아낸다. 여기서는 eno1 이라 한다.
```bash
$ ifconfig
eno1: flags...
...
```
2. /etc/netplan/에 있는 default 설정 파일을 열고 필요한 정보를 입력한다.
```bash
$ sudo vi /etc/netplan/~~~.yaml

network:
  version: 2
  renderer: NetworkManager # 기본 적으로 여기까지는 적혀 있음.
  ethernets:
    eno1: # 이 유선 Device에 설정할 것이다.
     dhcp4: no # DHCP 설정 안한다.
     addresses: [고정IP/CIDR] # A.B.C.D/24 이런 형태
     gateway4: E.F.G.H # 게이트웨이 IP
     nameservers: # 네임 서버들...
       addresses: [I.J.K.L, M.N.O.P] # 네임 서버 IP list, 1개만 있을 수도 있고, 여러대 있을 수도 있다.
```
3. 변경사항을 적용한다.
```bash
$ sudo netplan --debug apply # --debug는 optional, 로그 보고 싶어서 넣었다.
...

$ ifconfig # 설정이 제대로 적용되었는지 확인.
...
```
* https://linuxconfig.org/how-to-configure-static-ip-address-on-ubuntu-18-04-bionic-beaver-linux
