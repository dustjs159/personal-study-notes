DNS - Domain Name System
=========================

### DNS 정의
* 사람이 기억하기 쉬운 도메인 이름을 IP 주소로 변환해주는 시스템
    * 도메인의 정의 : 네트워크 상에서 사람이 보다 쉽게 식별할 수 있는 문자로 구성되어 있는 호스트의 주소.

### DNS의 중요성
만약 DNS가 없다면 특정 웹 페이지에 접속하기 위해서 해당 웹 서버의 IP 주소를 알고 있어야 할 것이다. 과거에는 웹 서버의 수가 많지 않았기에 일일이 IP 주소를 기억하거나 수첩에 적어두는 등의 방법이 있었겠지만 현대 사회에서는 사실상 불가능한 일이다. 

따라서 DNS는 사람이 읽고 기억하기 쉬운 형태(예시로 `github.com`)로 웹 페이지에 접속할 수 있도록 도와주기에 매우 중요한 역할을 한다고 볼 수 있다.

### DNS 기본 동작 과정
웹 브라우저에 도메인을 입력한 순간부터 목적지 웹 페이지의 IP 주소를 반환받는 과정

1. 로컬 DNS 캐시 확인
2. `/etc/hosts` 파일 확인
    - `/etc/hosts` : 도메인 이름과 IP가 매핑되어 있는 파일로써 DNS 쿼리 과정에서 가장 먼저 참조하는 파일. 해당 파일에 도메인과 IP를 매핑시켜놓은 정보가 있다면 더 이상 Public DNS 서버에 쿼리하지 않고 파일에 지정된 IP를 반환받는다.
3. 디바이스에서 지정한 Public DNS 서버에 쿼리 시작
    - Root DNS 서버 쿼리
        - 바로 아래 계층의 TLD 정보만을 반환
    - TLD(Top Level Domain) DNS 서버 쿼리
        - TLD : root 바로 아래 단계의 계층으로써 조직의 특성(`.com`, `.io` 등)이나 국가 코드(`.kr`, `.jp` 등)가 여기에 해당됨.
        - 아래 계층에 대한 정보 반환
    - Authoritative DNS 서버 쿼리
        - 도메인 호스팅 업체가 여기에 해당
        - 여기서 호스팅 업체의 host zone에 등록된 레코드를 확인하여 해당 도메인의 IP를 반환.

### DNS 구조
![DNS](https://user-images.githubusercontent.com/57285121/115060392-c5baf300-9f22-11eb-8b78-70527a4f04ba.PNG)
* DNS의 구조는 Root DNS 부터 그 하위 도메인까지 계층구조로 구성되어 있으며 각 계층은 하위 도메인에 관한 정보를 갖고 있음
* Root DNS 서버 : 하위 계층인 TLD 정보만을 갖고 있으며 요청받은 도메인의 TLD를 확인하고 해당 TLD DNS 서버의 정보를 반환함
    * ICANN(국제 인터넷 주소 관리 기구)에서 관리
* TLD(Top Level Domain) DNS 서버 : Root DNS 바로 아래에 위치하는 최상위 도메인
    * gTLD(generic) : 조직의 특성에 따라 구분. e.g. `.com, .info, .org `등
    * ccTLD(country code) : 국가 코드. e.g. `.kr, .jp, .us` 등
* Authoritative DNS 서버 : 해당 도메인을 실제로 소유하고 있는 DNS 서버

### DNS 레코드 유형
* NS(Name Server) : 도메인을 소유한 실제 네임 서버 정보
    * 네임 서버란, 해당 도메인을 소유한 DNS 서버를 말한다.
* A : IPv4 주소
* AAAA : IPv6 주소
* CNAME(Canonical Name) : 도메인의 Alias

(이 외에도 여러가지 있음)
  
### DNS 세부 동작 과정
![dns3](https://user-images.githubusercontent.com/57285121/115513296-dfab5b80-a2bd-11eb-9374-469e9c97ba1c.PNG) 

1. 클라이언트는 브라우저를 통해서 도메인을 입력하면
    * 로컬 DNS 캐시를 확인 후 DNS 캐시가 없다면, 
    * `/etc/hosts` 파일에서 입력한 도메인과 매핑된 IP를 먼저 찾고 `/etc/hosts`에 매핑된 정보가 없다면,
    * 디바이스에 지정된 Public DNS 서버에게 도메인 주소에 해당하는 IP 주소 반환 요청을 한다. **(브라우저 → Public DNS 서버)**

2. Public DNS 서버는 Root DNS 서버 (".")에 쿼리 **(Public DNS 서버 → Root DNS 서버)**

3. Root DNS 서버는 요청 받은 도메인의 TLD(Top Level Domain)를 확인하고 해당 TLD DNS 서버의 IP 주소를 반환 **(Root DNS 서버 → Public DNS 서버)**
    * `.com`, `.io` 등등

4. Public DNS 서버는 Root DNS 서버로부터 응답받은 TLD DNS 서버에게 다시 IP 주소를 쿼리 **(Public DNS 서버 → TLD DNS 서버)**

5. TLD DNS 서버는 요청받은 도메인을 소유한 Authoritative DNS 서버를 확인하고 해당 Authoritative DNS 서버의 IP 주소를 반환 **(TLD DNS 서버 → Public DNS 서버)**

6. Public DNS 서버는 TLD DNS 서버로부터 응답받은 Authoritative DNS 서버에게 다시 IP 주소 쿼리 **(Public DNS 서버 → Authoritative DNS 서버)**

7. Authoritative DNS 서버는 보유한 레코드중에 요청한 도메인이 있는지 확인하고 있다면 해당 도메인의 IP 주소를 반환한다. 레코드에 없는 도메인이라면 `NXDOMAIN`을 반환 **( Authoritative DNS 서버 → Public DNS 서버)**

8. Public DNS 서버는 브라우저에게 IP 주소 반환 **(Public DNS 서버 → 브라우저)**

9. 웹 브라우저는 전달 받은 IP 주소에 https GET 요청.

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


