Linux Network Command
====================================
## Summary
- Last Updated : 21.06.16 Fri   
- Updated by : 윤연선
-----------------------------------

# 리눅스에서 네트워크 장치 이름
* CentOS 7은 NIC 이름을 ens32 또는 ens33으로 할당
* 이전 버전에서는 eth0, eth1로 인식
## 디바이스명 규칙
   
<img width="474" alt="스크린샷 2021-06-18 오전 3 51 14" src="https://user-images.githubusercontent.com/57285121/122456369-6fccff00-cfe8-11eb-8a3b-80905c5a8750.png">
   
* systemd에 의해 결정
* 인터페이스 타입   
> * en : Ethernet   
> * wl : 무선 LAN   
> * ww : 무선 WAN   
* 슬롯별 설정(랜카드 인터페이스 슬롯 번호)   
> * MAC주소 방식 표기 : x<MAC> ex) enxb32fd2ads..  
 
# 주요 네트워크 설정 파일
* /etc/sysconfig/network-scripts/ifcfg-<NIC name>
   
<img width="386" alt="스크린샷 2021-06-18 오전 2 24 17" src="https://user-images.githubusercontent.com/57285121/122445216-49a16200-cfdc-11eb-8cac-624d0ca7b595.png">
   
> * NIC 장치에 설정된 네트워크 정보가 들어있는 파일   
> * TYPE : 장치 타입   
> * PROXY_METHOD : 프록시 관련 설정   
> * BOOTPROTO : IP 할당 타입(none : 없음, **static : 고정**, dhcp : 동적)   
> * DEFROUTE : default gateway 사용 여부   
> * IPV4_FAILURE_FATAL : dhcp를 통한 IP 자동할당 실패 시 네트워크 종료 여부   
> * NAME : NIC 별칭   
> * UUID : NIC 구분을 위한 NIC 장치 ID   
> * DEVICE : NIC 장치 인식명   
> * ONBOOT : 부팅 시 NIC 자동 활성화 여부   

* 고정 IP 설정을 위해서 추가할 항목   
> * IPADDR=고정 IP 주소   
> * NETMASK=Netmask 주소   
> * GATEWAY=Gateway 주소   

* 설정한 NIC 장치 비활성화 : ``ifdown 장치 이름``
* 설정한 NIC 장치 활성화 : ``ifup 장치 이름``

* /etc/resolv.conf   
> * DNS 네임서버의 정보가 들어있는 파일   

* 설정 파일 수정 후에는 네트워크를 재시작 : `systemctl restart network`

# 네트워크 주요 명령어

## nmtui
   
<img width="735" alt="스크린샷 2021-06-18 오전 1 32 39" src="https://user-images.githubusercontent.com/57285121/122437850-127b8280-cfd5-11eb-9ee8-c653e3d83847.png">
   
* Network Manager Text User Interface
* /etc/NetworkManager에 있음
* /usr/lib/systemd/system에 데몬 등록
* 네트워크와 관련된 작업들을 직접 관리
* 실행 : ``nmtui``
* 변경 사항을 반영할 때는 반드시 재시작해야함
* 시작, 중지, 재시작, 상태 확인 : `systemctl start/stop/restart/status Networkmanager`

## netstat
* network statistics   
* 네트워크 접속, 라우팅 테이블, 네트워크 인터페이스의 통계 정보를 보여주는 도구
* 자주 쓰이는 옵션 : ``netstat -nlpt`` (연결 대기중인 tcp 프로토콜을 사용하는 프로그램 이름 목록)
   
<img width="885" alt="스크린샷 2021-06-03 오전 2 52 14" src="https://user-images.githubusercontent.com/57285121/120528705-b6323380-c416-11eb-9f94-c40581c1ae6d.png">
   
* 구성   
> * Proto : 프로토콜   
> * Recv-Q : 수신하고 있는 데이터중 처리하지 못하고 수신만 하고있는 데이터   
> * Send-Q : 전송하였으나 아직 전송되지 못하고 있는 데이터   
> * Local Address : Source IP, Port   
> * Foreign Address : Destination IP, Port   
* 옵션   
> * -l (listen) : 연결 대기중인 상태   
> * -n (port number) : 포트 번호   
> * -t (tcp) / -u (udp)   
> * -p : 프로그램 이름(PID)   
* 상태(State)   
> * LISTEN : 접속 요청 대기중   
> * ESTABLISHED : 세션 수립이 완료되어 통신이 이루어지고 있음   
> * FIN_WAIT1 : 클라이언트가 세션 종료를 요청(FIN)한 상태   
> * FIN_WAIT2 : 서버가 클라이언트의 최종 연결 종료 응답을 기다리는 상태   
> * SYN_SENT : 클라이언트가 서버에 연결 요청을 한 상태   
> * SYN_RECEIVED : 클라이언트에게 응답을 전달(SYN+ACK)했지만 클라이언트의 응답(ACK)이 오지 않은 상태   
> * CLOSED : 연결 종료   

## ifconfig
* inteface configuration
* 네트워크 인터페이스 구성 확인
   
<img width="701" alt="스크린샷 2021-06-03 오전 3 27 11" src="https://user-images.githubusercontent.com/57285121/120533331-97826b80-c41b-11eb-9d57-afd892f03469.png">
   
* 구성   
> * ens33 : 네트워크 인터페이스 이름   
> * flags : 네트워크 카드 상태    
> * mtu : 네트워크 인터페이스의 최대 전송 단위   
> * **inet : 네트워크 인터페이스에 할당된 IP 주소**   
> * netmask : 넷마스크 주소   
> * broadcast : 브로드캐스트 주소   
> * inet6 : IPv6 주소   
> * prefixlen : 서브넷 마스크로 사용될 비트 수   
> * RX packets : 수신 패킷 정보   
> * TX packets : 전송 패킷 정보   
* 옵션   
> * -a (all) : 비활성화된 네트워크 인터페이스까지 확인   

## ping
* 목적지를 향해 일정 크기의 패킷을 전송한 후 목적지로부터 오는 응답 메시지를 통해 네트워크 상태를 점검
* **ICMP 프로토콜을 사용함**
   
<img width="552" alt="스크린샷 2021-06-03 오전 3 52 27" src="https://user-images.githubusercontent.com/57285121/120536465-1f1da980-c41f-11eb-9bc0-7272f9e890e7.png">
   
* 구성   
> * ttl(time-to-live) : 패킷이 네트워크 상에서 살아있는 시간(라우터 하나 지날 때마다 하나씩 감소)   
> * time : 응답이 오기까지 걸리는 시간   
* 옵션   
> -c [n] : n개의 패킷만 전송   

## firewalld
* firewalld : CentOS 7부터 채택된 **패킷 필터링**
* CentOS 6까지는 iptables에서 실행
* Linux 커널의 Netfilter의 동작(패킷 필터링)을 설정 및 관리
* iptables는 체인(INPUT, OUTPUT, FORWARD)마다 패킷 필터링을 적용
* firewalld는 zone(default : public)이라는 그룹 단위로 규칙을 정의
* iptables는 변경된 규칙을 적용하기 위해서는 서비스를 재시작해야함(서비스가 일시적으로 중단)
* firewalld는 임시 규칙, 지속적 규칙을 각각 관리할 수 있으며 서비스 재시작 없이 변경사항을 반영할 수 있음
* firewalld : **동적인 설정이 가능**
   
|기능|명령어|
|------|---|
|방화벽 실행 여부 확인|firewall-cmd --state|
|모든 zone의 정책 확인|firewall-cmd --list-all|
|정의된 서비스 목록 확인|firewall-cmd --get-services|
|허용된 서비스 목록 확인|firewall-cmd --list-services|
|변경 사항을 적용(리로드)|firewall-cmd --reload|
|영구적으로 서비스 등록|firewall-cmd --permanent --zone=<zone이름> --add-service=<서비스이름>|
|정의된 서비스 목록 확인|firewall-cmd --get-services|
|허용된 서비스 확인|firewall-cmd --list -services|
   
* /usr/lib/firewalld/services에 직접 xml파일을 만들어서 저장해서 서비스 사용 가능

## route
* 라우팅 테이블 수정 및 확인
   
<img width="721" alt="스크린샷 2021-06-13 오전 10 40 00" src="https://user-images.githubusercontent.com/57285121/121792752-b65eda00-cc33-11eb-8609-d255458f1b6f.png">
   
> * Gateway : 외부 네트워크와 연결하기 위한 게이트웨이 주소   
> * Genmask : 목적지 네트워크의 넷마스크 주소(0.0.0.0 : default gateway)   
> * Flags : 경로에 대한 정보(U : 살아있는 경로, G : 게이트웨이를 향하는 경로)   
> * Metric : 목적지 네트워크까지 거리   
> * Ref : 경로 참조 횟수   
> * Use : 경로 탐색 횟수   
> * Iface : 네트워크 인터페이스   
