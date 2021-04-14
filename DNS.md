DNS
===================================
DNS(Domain Name System)
-----------------------------------
# 개요
* 도메인 이름과 IP주소를 변환하는 역할   
* 영어/한글 주소를 네트워크에서 찾아갈 수 있는 IP로 변환해 주는 시스템   
* 이 DNS를 운영하는 서버를 Name Server라고 함   
* Name Server는 모든 PC의 URL과 IP 정보를 저장함   
* 포트번호는 53번을 사용   
 
# 과정
1. 클라이언트는 웹 브라우저에 접속하고자 하는 사이트의 도메인 이름(www.naver.com등)을 입력
2. DNS 서버(Name Server)가 해당 도메인 이름과 일치하는 IP주소를 찾고 접속을 가능하게 해줌

# 구성요소
* DNS는 전 세계 분산형 DB 구조로 동작   
1. Domain Name Space / Resource Record : 주소 체계 및 도메인 내 정보   
2. Name Server : 도메인 별 정보를 가지고 있는 서버 역할 (Resolver의 쿼리에 정보 전달)   
3. Resolver(Client S/W) : 도메인 정보를 요청받아 쿼리하여 Caching   

# DNS Resource Record(RR)
* DNS는 리소스 레코드를 가지고 있으며 이 레코드는 
* Forward Zone(Domain Name → IP) : 도메인을 구성하는 호스트에 대한 정보   
* Reverse Zone(IP → Domain name) : DNS서버 자신에 대한 정보를 기록   
