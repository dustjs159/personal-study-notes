Firewall
========================


# Firewall(방화벽) : **침입 차단 시스템**
* 네트워크 상에서 트래픽의 출입을 제어하는 장치 혹은 소프트웨어
* 네트워크 트래픽을 모니터링하고 미리 정의된 규칙을 기준으로 특정 트래픽을 허용 또는 차단함
* 외부로부터 내부망을 보호하기 위해서 혹은 내부망의 정보유출을 방지하기 위해 사용
* **ACL(Access Control List)**를 통해 네트워크 상에서 트래픽에 대한 보안 정책을 설정   

# ACL(Access Control List)
* 허가되지 않은 사용자들의 네트워크 트래픽을 차단하기 위해 참조하는 목록   
* Standard ACL : 패킷(트래픽)의 Source IP 주소만을 확인 후 트래픽 차단 여부 결정
* Extended ACL : L3 헤더의 Source IP 주소 뿐 아니라 Destination IP 주소, 프로토콜 정보, TTL 그리고 L4 헤더의 Source Port 번호와 Destination Port 번호 등의 정보까지도 확인하여 트래픽 차단 여부 결정   
<img width="667" alt="스크린샷 2021-05-19 오후 11 44 21" src="https://user-images.githubusercontent.com/57285121/118833106-28c1f000-b8fc-11eb-8dff-ff45d3f9da96.png">   

# 방화벽 운영 정책
* Deny All 정책 : 모든 트래픽을 먼저 차단하고 허용해야 할 트래픽을 선별적으로 허용(외부 -> 내부)
* Permit All 정책 : 모든 트래픽을 허용하고 특정 트래픽만 선별적으로 차단(내부 -> 외부)
  
# Inbound / Outbound   

|Inbound|Outbound|
|----------|-------------|
|내부를 향함|외부를 향함|
|서버 내부로 들어오는 트래픽(진입)|서버 외부로 나가는 트래픽(송출)|
|클라이언트->서버|서버->클라이언트|
|클라이언트가 업로드 할 때|클라이언트가 다운로드 할 때|   
   
* Inbound 규칙으로 지정한 조건에 맞는 트래픽은 방화벽을 정상적으로 통과하여 네트워크 트래픽(데이터)이 서버에 도착   
> * 기본설정 : 모든접속 차단   
> * **Deny All 정책**   
* Outbound 규칙으로 지정한 조건에 맞는 트래픽은 방화벽을 정상적으로 통과하여 네트워크 트래픽(데이터)이 클라이언트에 도착   
> * 기본설정 : 모든접속 허용   
> * **Permit All 정책**

# 방화벽 주요 기능
* 접근 제어(Access Control)   
> * **패킷 필터링**을 통해 외부에서 내부 네트워크로 접근을 통제함   
> * **Stateless** : 패킷이 들어올 때 마다 ACL을 참조하여 해당 트래픽을 차단 및 허용하는 방법(패킷의 헤더만 확인)   
> * **Stateful** : 한번 허용된 패킷의 정보를 기억하고 해당 패킷이 다시 들어올 때 트래픽을 허용하는 방법(상위 계층의 정보까지 확인)

* 사용자 인증(Authentication)   
> * 방화벽은 내/외부 네트워크 간 접속점   
> * 방화벽을 지나기 위해서는 사용자들의 신분 증명이 필요함   
> * ID/PW, 인증서 등을 이용해 사용자를 검증하는 방식

* 로깅과 감사(Logging & Auditing)   
> * 접속하는 모든 트래픽의 정보를 기록(로깅)과 추적(감사)   
> * 방화벽 관리자는 기록된 로그를 바탕으로 보안 관리 기능을 설정해야함

* 주소 변환(NAT : Network Address Translation)   
> * 내부 사설 IP 주소로 공용 인터넷 망과 통신하기 위해 공인 IP 주소로 변환   
> * 외부 인터넷상의 사용자들은 내부의 사설 IP 주소를 알 수 없음(보안성)   

* **네트워크의 트래픽 통과 및 데이터 접근을 제한함으로써 외부 침입으로부터 보호하고 정보 유출을 막는다(전반적으로 보안성이 가장 핵심)**


# 방화벽 종류
## Packet Filtering
* 1세대 방화벽. **Stateless**
* Layer 3, 4(Network, Transport)에서 동작하는 방식
* 지나가는 패킷의 Source / Destination IP Address + 각 서비스의 Port 번호를 이용해 접근 제어(Extended ACL)
* 장점   
> * 패킷의 IP 주소 및 Port번호만을 확인하여 접근 제어하기 때문에 속도가 빠르다   
* 단점   
> * IP 주소와 Port번호 외 세부 데이터를 확인하지 않기 때문에 악의적으로 조작된 데이터를 걸러내지 못함   
> * Extended ACL의 항목이 많아질 수록 방화벽에 부하가 생길 수 있음   

## Application Gateway
* 2세대 방화벽. **Proxy 방화벽**
* Layer 7(Application)에서 동작
* 지나가는 패킷의 TCP/IP 헤더 뿐만 아니라 패킷 속 실제 데이터도 확인하여 접근 제어
* 클라이언트와 서버 사이에 서비스 별 **Proxy**가 포함된 **Bastion Host**를 두고, 각 서비스의 요청에 대해 ACL을 적용하고 그에 따라 트래픽 허용 및 차단
* **Bastion Host** : 침입 차단 소프트웨어가 설치된 호스트
* 외부 네트워크와 내부 네트워크는 반드시 Bastion Host(Proxy)를 통해서만 연결이 되어야 함   
* 외부 네트워크와 내부 네트워크가 직접적인 연결을 하지 않기 때문에 내부 네트워크의 정보를 숨길 수 있음
* Proxy가 패킷의 데이터까지 확인 후 이상이 없다면 목적지에 전송   
<img width="446" alt="스크린샷 2021-05-20 오전 2 03 22" src="https://user-images.githubusercontent.com/57285121/118854250-90ce0180-b90f-11eb-928f-d9cf906bb77c.png">   

* 장점   
> * Proxy를 통한 연결이기 때문에 내부 네트워크에 대한 정보를 숨길 수 있음(보안성)   
> * 패킷 속 데이터까지 확인하기 때문에 패킷 필터링보다 높은 보안 설정이 가능함   
* 단점   
> * 패킷 속 데이터까지 확인하는 과정에서 많은 부하가 발생할 수 있음   
> * 새로운 서비스를 제공하기 위해 Proxy서버를 증설해야함   
> * 미리 정의된 Application만 수용이 가능하기 때문에 네트워크 구성에 있어서 유연함이 떨어짐   

## Circuit Gateway
* 2세대 방화벽. **Proxy 방화벽**
* Layer 5 ~ 7(Session ~ Application) 사이에서 동작
* 지나가는 패킷의 실제 데이터를 제외한 패킷의 모든 부분을 확인하여 접근 제어
* 각 서비스 별 Proxy를 두는 Application Gateway와는 다르게 하나의 Proxy를 둠
* 하나의 Proxy는 어느 서비스라도 이용할 수 있는 통합적인 Proxy형태로 이용(Generic Proxy)
* 클라이언트에는 Generic Proxy에 접속하기 위한 별도의 프로그램을 설치해야 함(Generic Proxy는 여러가지 서비스를 이용할 수 있기 때문에)   
<img width="432" alt="스크린샷 2021-05-20 오전 2 07 37" src="https://user-images.githubusercontent.com/57285121/118854887-29648180-b910-11eb-8388-948e2a80c2a4.png">   

* 장점   
> * 실제 데이터에 대한 확인을 하지 않기 때문에 Application Gateway보다 처리 속도가 빠름   
* 단점   
> * Generic Proxy를 통과하기 위한 클라이언트 프로그램을 별도로 설치해야하기 때문에 번거로움   
> * Application Gateway보다 보안성이 떨어짐(실제 데이터는 확인하지 않기 때문에)   

## Stateful Inspection
* 3세대 방화벽. **Stateful**
* Packet Filtering과 같은 패킷 정보(TCP/IP 헤더)를 검색하지만 추가적으로 TCP 연결에 관한 정보를 기록(Packet Filtering + Sesseion 추적)
* 한번 허용된 패킷의 정보를 테이블에 등록하고 해당 패킷이 다시 들어올 때 테이블 정보를 참조하여 패킷을 통과시킴
* 
# 방화벽 구조
## Screening Router
## Single-Homed Gateway
## Dual-Homed Gateway
## Screened Host Gateway
## Screened Subnet Gateway

