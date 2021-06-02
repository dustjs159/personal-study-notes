Linux Network Command
====================================
## Summary
- Last Updated : 21.06.02 Wed   
- Updated by : 윤연선
-----------------------------------

# netstat
* network statistics   
* 네트워크 접속, 라우팅 테이블, 네트워크 인터페이스의 통계 정보를 보여주는 도구
   
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
* 자주 쓰이는 옵션 : ```netstat -nlpt``` (연결 대기중인 tcp 프로토콜을 사용하는 프로그램 이름 목록)

# ifconfig
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
* 네트워크 인터페이스 비활성화 : ```ifdown 네트워크인터페이스 이름```
* 네트워크 인터페이스 활성화 : ```ifup 네트워크인터페이스 이름```
 
# ping
* 목적지를 향해 일정 크기의 패킷을 전송한 후 목적지로부터 오는 응답 메시지를 통해 네트워크 상태를 점검
* **ICMP 프로토콜을 사용함**
   
<img width="552" alt="스크린샷 2021-06-03 오전 3 52 27" src="https://user-images.githubusercontent.com/57285121/120536465-1f1da980-c41f-11eb-9bc0-7272f9e890e7.png">
   
* 구성   
> * ttl(time-to-live) : 패킷이 네트워크 상에서 살아있는 시간(라우터 하나 지날 때마다 하나씩 감소)   
> * time : 응답이 오기까지 걸리는 시간   
* 옵션   
> -c [n] : n개의 패킷만 전송   

# top
* 실시간 CPU 점유율 확인

# ps
* Process Status
* 실행중인 프로세스의 목록 확인

# route
* 라우팅 테이블 추가 / 제거


