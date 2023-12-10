DNS - Domain Name System
=========================

### Definition
* 사람이 기억하기 쉬운 도메인 이름을 IP 주소로 변환해주는 시스템

### DNS 동작 과정
웹 브라우저에 도메인을 입력한 순간부터 목적지 웹 페이지의 IP 주소를 반환받는 과정

1. 로컬 DNS 캐시 확인
2. `/etc/hosts` 파일 확인
    - `/etc/hosts` : 도메인 이름과 IP가 매핑되어 있는 파일로써 DNS 쿼리 과정에서 가장 먼저 참조하는 파일. 해당 파일에 도메인과 IP를 매핑시켜놓은 정보가 있다면 더 이상 외부 DNS 서버에 쿼리하지 않고 파일에 지정된 IP를 반환받는다.
3. 디바이스에서 지정한 외부 DNS 서버에 쿼리 시작
    - 최상위 root 도메인 (".") 쿼리
        - 바로 아래 계층의 TLD 정보만을 반환
    - TLD(Top Level Domain) 쿼리
        - TLD : root 바로 아래 단계의 계층으로써 조직의 특성(`.com`, `.io` 등)이나 국가 코드(`.kr`, `.jp` 등)가 여기에 해당됨.
        - 아래 계층에 대한 정보 반환
    - Authoritative DNS 쿼리
        - 도메인 호스팅 업체가 여기에 해당
        - 여기서 호스팅 업체의 host zone에 등록된 record를 확인하여 해당 도메인의 IP를 반환.

### DNS 구조와 record 구성요소
![DNS](https://user-images.githubusercontent.com/57285121/115060392-c5baf300-9f22-11eb-8b78-70527a4f04ba.PNG)
* DNS의 구조는 최상위 root 도메인부터 그 하위 도메인까지 계층구조로 구성되어 있음.
  * 각 층의 domain name space는 도메인과 그 하위 도메인에 관한 정보를 트리구조로 관리
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
  
### DNS 세부 동작 과정

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

### 관련 명령어
* `nslookup` : 네임 서버에 특정 도메인의 IP를 질의
```
$ nslookup {domain}

# 대화형으로도 가능    
$ nslookup
> {domain}
```

* `dig` : DNS Record 조회

```
$ dig {domain}
```


