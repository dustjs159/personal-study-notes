💻 [Network] DNS
=========================

# 💡 DNS(Domain Name System)

* 호스트의 도메인 이름과 IP주소를 매핑
  * 이를 통해 웹 페이지에 접속할 때 IP주소를 입력하지 않고도 도메인 이름을 입력하여 해당 웹 페이지 IP에 접근
  * 띄우고자 하는 웹 페이지, 즉 웹 서버의 IP를 일일이 기억하고 입력할 필요가 없음
* 도메인 이름 ↔️ IP 주소 변환을 담당하는 서버 : **Name Server**
  * Name Server는 도메인과 IP 매핑 정보를 저장함
* Port : 53
 

## 📌 DNS 동작 과정

![dns3](https://user-images.githubusercontent.com/57285121/115513296-dfab5b80-a2bd-11eb-9374-469e9c97ba1c.PNG) 

1. 클라이언트는 브라우저를 통해서 도메인을 입력하면 `/etc/hosts` 파일에서 입력한 도메인과 매핑된 IP를 먼저 찾고 `/etc/hosts`에 매핑된 정보가 없다면 ISP의 DNS 서버에게 도메인 주소에 해당하는 IP 주소를 Request

2. ISP DNS 서버에서 캐시 데이터를 확인하고 캐시가 없다면 Root DNS 서버에게 IP 주소를 Request(캐시가 있다면 8.로 건너 뜀)

3. Root 서버는 요청 받은 도메인의 TLD(Top Level Domain)를 확인하고 TLD DNS 서버의 주소를 Response

4. ISP DNS 서버는 TLD DNS 서버에게 다시 IP 주소를 Request

5. TLD DNS 서버는 요청한 도메인의 Hostname을 확인하고 해당 Hostname을 관리하는 Authoritative DNS 서버의 주소를 Response

6. ISP DNS 서버는 Authoritative DNS 서버에게 또 다시 IP 주소 Request

7. Authoritative DNS 서버는 Namespace에 요청받은 도메인이 있는지 확인하고 해당 도메인에 매핑된 IP 주소를 확인하고 Response. 동시에 ISP DNS 서버는 해당 정보를 캐시에 저장

8. ISP DNS 서버는 브라우저에게 IP 주소 Response

9. 웹 브라우저는 전달 받은 IP 주소를 갖고 있는 호스팅 서버에게 웹 사이트 접속 Request

10. 웹 사이트 접속, 웹 페이지 출력

## 📌 DNS 구성 요소
* Domain Name Space & Resource Record
* Name Server
* Resolver(해석기)

### ✔️ Domain Name Space & Resource Record
* Domain Name Space : DNS가 저장, 관리하는 계층적 자료구조
  * 각 층의 Domain Name Space는 도메인과 그 하위 도메인에 관한 정보를 트리구조로 관리
![DNS](https://user-images.githubusercontent.com/57285121/115060392-c5baf300-9f22-11eb-8b78-70527a4f04ba.PNG)
  * Root : TLD 정보만을 갖고 있으며 요청받은 도메인의 TLD를 확인하고 해당 TDL DNS 서버의 정보를 반환함
    * ICANN(국제 인터넷 주소 관리 기구)에서 관리
  * TLD(Top Level Domain) : Root 바로 아래에 위치하는 최상위 도메인
    * gTLD(generic) : 조직의 특성에 따라 구분. e.g. `.com, .info, .org `등
    * ccTLD(country code) : 국가 코드. e.g. `.kr, .jp, .us` 등
  * 그 아래 계층의 서브 도메인은 호스팅 업체가 관리 
* Resource Record : Domain Name Space의 트리구조에서 각 노드에 포함된 도메인의 Type  
  * A : IPv4 주소   
  * AAAA : IPv6 주소
  * CNAME(Canonical Name) : 도메인의 Alias
  * NS(Name Server) : 네임 서버의 역할을 다른 서버에게 위임
  * MX(Mail Exchange) : 메일 서버
  * SOA(Start Of Authority) : 권한 시작 레코드; →  DNS영역의 메인DNS서버를 정의하고 영역의 변경사항을 기록하고 영역의 기본 TTL(Time To Live)값을 정의   
  

### ✔️ Name Server
* 도메인 이름을 IP주소로 변환하기 위한 Domain Name Space + Resource Record의 데이터를 갖고 있는 서버
* Resolver로부터 요청받은 도메인 이름에 대한 IP정보를 다시 Resolver로 전달

### ✔️ Resolver(Client S/W)
* 클라이언트의 요청을 네임 서버로 전달 및 네임 서버로부터 도메인 이름과 IP주소를 받아 클라이언트에게 제공
* 네임 서버에 요청을 했을 때, 해당 서버의 정보가 없으면 다른 네임 서버에게 요청을 보내 정보를 받아온다


## 📌 관련 명령어
* `nslookup` : 네임 서버에 특정 도메인의 IP를 질의
  * `$ nslookup {domain}`
  * 대화형으로도 가능
* `dig` : DNS Record 조회
  * `$ dig {domain}`