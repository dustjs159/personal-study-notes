DNS
===================================
DNS(Domain Name System)
-----------------------------------
# DNS 개요
* 도메인 이름과 IP주소를 변환하는 역할   
* 영어/한글 주소(도메인)를 네트워크에서 찾아갈 수 있는 IP로 변환해 주는 시스템   
* 이 DNS를 운영하는 서버를 Name Server라고 함   
* Name Server는 모든 PC의 URL과 IP 정보를 저장함   
* 포트번호는 53번을 사용   
 
# DNS의 대략적인 동작원리   
![dns1](https://user-images.githubusercontent.com/57285121/115509710-b983bc80-a2b9-11eb-8626-bc8d7ff30ad0.PNG)   
1. 클라이언트가 웹 브라우저에 도메인 이름(Netsite.com)검색   
2. DNS 서버로 도메인 이름 전달
3. DNS서버는 내부에서 도메인 이름에 맞는 IP주소를 찾고 클라이언트에게 IP주소를 가지고 호스팅 서버(해당 웹 사이트의 데이터가 저장된 서버)로 이동하라고 요청
4. 웹 브라우저가 다시 IP주소로 접속해서 웹 사이트가 출력이 됨

# DNS 구성요소
* DNS는 전 세계 분산형 DB 구조로 동작   
* Domain Name Space   
> * DNS가 저장, 관리하는 계층적 자료구조   
  
![DNS](https://user-images.githubusercontent.com/57285121/115060392-c5baf300-9f22-11eb-8b78-70527a4f04ba.PNG)   
   
> * 최상위에 루트 DNS서버가 존재하고 그 밑으로 인터넷에 연결된 노드가 연속해서 이어진 계층구조로 구성   
> * 각 층의 도메인들은 그 하위 도메인에 관한 정보를 관리하는 구조   

* Resource Record
> * 도메인에 대한 설정을 담당하는 zone파일에 등록하는 도메인의 타입
> * 도메인 이름에 설정할 수 있는 데이터 타입들   
> * A(Host) : 주소/호스트 레코드; →  호스트와 IPv4주소를 매핑   
> * AAAA : 주소 레코드; →  호스트와 IPv6주소를 매핑   
> * CNAME(Canonical Name) : 별칭 레코드; →  실제 호스트명의 별칭을 정의   
> * MX(Mail eXchange) : 메일 교환 레코드; →  메일서버에 도착할 수 있는 라우팅 정보 제공   
> * SRV(SeRVice) : 서비스 위치 레코드; →  비슷한 TCP/IP 서비스를 제공하는 다수의 서버 위치 정보 제공   
> * SOA(Start Of Authority) : 권한 시작 레코드; →  DNS영역의 메인DNS서버를 정의하고 영역의 변경사항을 기록하고 영역의 기본 TTL(Time To Live)값을 정의   
> * NS(Name Server) : 네임 서버 레코드; →  DNS 영역의 DNS서버의 목록

* Name Server  
> * 영어/한글로 표현된 도메인 이름을 IP주소로 변환하기 위한 Domain NameSpace의 데이터를 갖고 있는 서버   
> * Resolver로부터 요청받은 도메인 이름에 대한 IP정보를 다시 Resolver로 전달

* Resolver(Client S/W)
> * 클라이언트의 요청을 네임 서버로 전달 및 네임 서버로부터 도메인 이름과 IP주소를 받아 클라이언트에게 >제공
> * 네임 서버에 요청을 했을 때, 해당 서버의 정보가 없으면 다른 네임 서버에게 요청을 보내 정보를 받아온다

# DNS 서버 종류  
* DNS서버 하나만으로는 사실상 운영 불가
* DNS서버 종류를 디렉토리/계층형태로 계층화해서 단계적으로 처리
* 도메인의 총 관리는 ICANN(국제 인터넷주소 관리 기구)에서 함   
![dns2](https://user-images.githubusercontent.com/57285121/115511329-b12c8100-a2bb-11eb-891a-b0d295ded98d.PNG)
* Root DNS Server : ICANN이 직접 관리. TLD DNS 서버의 IP들을 저장해두고 안내하는 역할.
* TLD(Top Level Domain) DNS Server : 도메인 등록 기관(Registry)이 관리. Authoritative DNS Server의 IP주소를 저장해두고 안내하는 역할. 도메인 업체의 DNS 변경 사항을 이 곳에 저장하기 때문에 Authoritative DNS Server의 정보를 알고있다.
* Authoritative DNS Server : 실제 개인 도메인과 IP주소의 관계가 기록, 저장, 변경되는 서버. 도메인/호스팅 업체의 Name Server, 개인 DNS Server가 여기에 해당.
* Recursive DNS Server : 클라이언트가 웹 사이트 접속시 가장 먼저 접근하는 DNS서버. 클라이언트가 자주 방문하는 주소의 정보를 캐시에 저장하는 서버. ISP(통신사.SK,KT,LG 등) DNS Server가 여기에 해당됨
* **브라우저는 캐시가 저장된 Recursive DNS Server를 사용하고 실제 Name Server를 설정하는 곳은 Authoritative Server.**

# DNS 동작 원리
    
![DNS2](https://user-images.githubusercontent.com/57285121/115060487-dff4d100-9f22-11eb-86ab-313cce828808.PNG)   
   
1. 1,2,3 : Root DNS 서버는 전체 도메인 정보는 알지 못하기 때문에 자신의 하위 Domain인 COM DNS 서버의 주소를 알려줌

2. 4, 5 : 이를 수신한 Local DNS 서버는 다시 com DNS 서버에게 정보를 요청하고, com DNS 서버도 자신의 하위 레벨 Domain인 naver.com의 DNS서버 주소를 알려줌

3. 6, 7 : 이를 수신한 Local DNS 서버는 다시 naver.com DNS 서버에게 www 호스트에 대한 정보를 요청하고, naver.com DNS 서버는 www.naver.com 에 대한 IP서버 주소를 알려줌

4. 8 : Local DNS 서버는 위와 같이 www.naver.com 에 대한 IP주소를 수신 후 자신의 DNS Cache에 등록하고 해당 정보를 요청했던 클라이언트에에게 응답 전송


# DNS 상세 동작 원리
   
![dns3](https://user-images.githubusercontent.com/57285121/115513296-dfab5b80-a2bd-11eb-9374-469e9c97ba1c.PNG)   


1. 클라이언트는 브라우저를 통해서 Nesite.com을 검색하고, 사용하고 있는 통신사인 KT DNS 서버(ISP DNS Server)에게 도메인 주소에 해당하는 IP 주소를 요청.

2. ISP DNS Server에선 캐시 데이터가 없다는 걸 확인하고 Root DNS 서버에게 어디로 가야 하는지 요청함(캐시가 있다면 8.로 건너 뜀.)

3. 루트 서버는 TLD DNS Server 주소만 관리하기 때문에, xx.com 도메인을 보고는 COM 최상위 도메인을 관리하는 TLD DNS Server 주소를 안내함.

4. ISP DNS Server는 COM 서버에게 어디로 가야 하는지 다시 요청함.

5. COM 서버는 gabia DNS 서버에서 해당 도메인이 관리되고 있는 걸 확인하고 안내함.

6. ISP DNS Server는 gabia 서버에게 또 다시 요청함.

7. gabia 서버는 “Nesite.com = 12.123.123.123”이라는 정보를 확인하고 이 IP를 알려줌. 동시에 ISP DNS Server는 해당 정보를 캐시로 기록해 둠.

8. ISP DNS Server는 브라우저에게 힘들게 알아 낸 12.123.123.123 주소를 안내함.

9. 웹 브라우저는 12.123.123.123 IP 주소를 갖고 있는 호스팅 서버에게 웹사이트를 출력하라고 요청함.

10. 웹 페이지 출력















  
