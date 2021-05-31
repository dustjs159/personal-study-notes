방화벽
========================
## Summary
- Last Updated : 21.05.25 Tue   
- Updated by : 윤연선
-----------------------------------

# Firewall(방화벽) : **침입 차단 시스템**
* 네트워크 상에서 트래픽의 출입을 제어하는 장치 혹은 소프트웨어
* 네트워크 트래픽을 모니터링하고 미리 정의된 규칙을 기준으로 특정 트래픽을 허용 또는 차단함
* 외부로부터 내부망을 보호하기 위해서 혹은 내부망의 정보유출을 방지하기 위해 사용
* **ACL(Access Control List)** 를 통해 네트워크 상에서 트래픽에 대한 보안 정책을 설정   

# ACL(Access Control List)
* 허가되지 않은 사용자들의 네트워크 트래픽을 차단하기 위해 참조하는 목록   
* Standard ACL : 패킷(트래픽)의 Source IP 주소만을 확인 후 트래픽 차단 여부 결정
* Extended ACL : L3 헤더의 Source IP 주소 뿐 아니라 Destination IP 주소, 프로토콜 정보, TTL 그리고 L4 헤더의 Source Port 번호와 Destination Port 번호 등의 정보까지도 확인하여 트래픽 차단 여부 결정
   
<img width="667" alt="스크린샷 2021-05-19 오후 11 44 21" src="https://user-images.githubusercontent.com/57285121/118833106-28c1f000-b8fc-11eb-8dff-ff45d3f9da96.png">
   
# 방화벽 운영 정책
* **Deny All 정책** : 모든 트래픽을 먼저 차단하고 허용해야 할 트래픽을 선별적으로 허용(외부 -> 내부)
* **Permit All 정책(Allow)** : 모든 트래픽을 허용하고 특정 트래픽만 선별적으로 차단(내부 -> 외부)
* Whitelist(Positive rule) : 모든 트래픽을 허용. 위험한 트래픽은 다 차단
* Blacklist(Negative rule) : 모든 트래픽을 차단. 안전한 트래픽만 허용

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

# Untrusted Zone / Trusted Zone
   
<img width="799" alt="스크린샷 2021-05-25 오전 1 09 32" src="https://user-images.githubusercontent.com/57285121/119375530-df0b4800-bcf5-11eb-9d5f-4435e514e437.png">
   
<img width="532" alt="스크린샷 2021-05-25 오전 1 28 14" src="https://user-images.githubusercontent.com/57285121/119377785-7bcee500-bcf8-11eb-91ed-c1716ef9415d.png">
   
* Untrusted Zone : 신뢰할 수 없는 지역(외부 네트워크)
* Trusted Zone : 신뢰할 수 있는 지역(내부 네트워크)
* 기본적으로 트래픽은 Untrusted Zone에서 Trusted Zone으로의 접근이 모두 차단됨(Deny ALL)
* 반대로 Trusted Zone에서 Untrusted Zone으로 나가는 것은 모두 허용됨(Permit ALL)

# 방화벽 주요 기능
* 접근 제어(Access Control)   
> * **패킷 필터링**을 통해 외부에서 내부 네트워크로 접근을 통제함   
> * **Stateless** : 패킷이 들어올 때 마다 ACL을 참조하여 해당 트래픽을 차단 및 허용하는 방법(패킷의 헤더만 확인)   
> * **Stateful** : 한번 허용된 패킷의 연결 정보(상태)를 기록하고 해당 패킷이 다시 들어올 때 연결 정보를 참조하여 트래픽을 허용하는 방법(상위 계층의 정보까지 확인)

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

# Stateless / Stateful
* 일반적으로 방화벽은 Inbound의 패킷은 Deny All 정책, Outbound의 패킷은 Permit All 정책 적용

## Stateless
* ACL을 참조
* ACL의 접근 규칙을 기반으로 패킷의 진입 허용 및 차단을 결정함
* Inbound와 Outbound의 접근 규칙이 각각 설정해야 함
* 상태를 저장하지 않고 한 번 방화벽을 통과한 Inbound 패킷은 나갈 때 Outbound의 접근 규칙을 적용받음
* 상태를 저장하지 않아 한 번 방화벽을 통과한 Outbound 패킷은 다시 들어올 때 Inbound의 접근 규칙을 적용받음
* 장점   
> * 패킷의 정보를 일부분만 확인하기 때문에 걸리는 시간이 적음(속도가 빠름)   
* 단점   
> * 방화벽에 부하가 많이 걸리게 될 수 있음   
> * 한번 들어왔던 패킷도 다시 패킷의 정보를 확인해야 함   

## Stateful
* 기존의 접근 규칙과 Stateful Flow Table을 참조
* Inbound의 접근 규칙만 설정(별도의 Outbound 접근 규칙을 만들 필요가 없음)
* 상태를 저장하여 한 번 방화벽을 통과한 Inbound 패킷은 나갈 때 Outbound의 접근 규칙 적용을 받지 않음
* 상태를 저장하여 한 번 방화벽을 통과한 Outbound 패킷은 다시 들어올 때 Inbound의 접근 규칙 적용을 받지 않음
* 장점   
> * Stateful Flow Table을 확인하여 지속적으로 세션의 상태를 모니터링 가능(지속적인 세션 점검)   
* 단점   
> * 방화벽 재 가동시 Stateful Flow Table의 정보가 훼손될 수 있기 때문에 정상적인 패킷도 거부될 수 있음   

## TCP에서 세션을 맺을 때 Stateful Flow Table
   
<img width="866" alt="스크린샷 2021-05-24 오후 11 28 12" src="https://user-images.githubusercontent.com/57285121/119362487-b714e800-bce7-11eb-809e-2dba7a3c9f6f.png">
   
* 3 way-handshake 과정(세션을 수립하는 과정)
1. 방화벽이 Untrusted Zone의 TCP SYN 패킷을 받아 접근 규칙을 확인하여 Trusted Zone으로 전달을 하고 이 때 방화벽은 Stateful Flow Table을 생성
2. Stateful Flow Table에 SYN의 정보(Source IP, Destination IP 등)를 기록
3. Trusted Zone에서는 요청받은 SYN 패킷에 응답하기 위해 SYN + ACK를 방화벽으로 전송(응답)
4. 방화벽은 Stateful Flow Table을 참조하여 처음 받았던 SYN에 응답하는 패킷임을 확인하고 Untrusted Zone에 전달

# 방화벽 종류
## Packet Filtering
* **Stateless**
* Layer 3, 4(Network, Transport)에서 동작하는 방식
* 지나가는 패킷의 Source / Destination IP Address + 각 서비스의 Port 번호를 이용해 접근 제어(Extended ACL)
* 장점   
> * 패킷의 IP 주소 및 Port번호만을 확인하여 접근 제어하기 때문에 속도가 빠르다   
* 단점   
> * IP 주소와 Port번호 외 세부 데이터를 확인하지 않기 때문에 악의적으로 조작된 데이터를 걸러내지 못함   
> * Extended ACL의 항목이 많아질 수록 방화벽에 부하가 생길 수 있음   

## Application Gateway
* **Proxy 방화벽**
* Layer 7(Application)에서 동작
* 지나가는 패킷의 TCP/IP 헤더 뿐만 아니라 패킷 속 실제 데이터도 확인하여 접근 제어
* 클라이언트와 서버 사이에 서비스 별 **Proxy**가 포함, 각 서비스의 요청에 대해 ACL을 적용하고 그에 따라 트래픽 허용 및 차단
* 외부 네트워크와 내부 네트워크는 반드시 Proxy를 통해서만 연결이 되어야 함   
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
* **Proxy 방화벽**
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
* **Stateful**
* 방화벽을 통과해서 들어왔던 적이 있는 패킷은 다시 통과할 수 있도록 함
* 패킷이 방화벽을 통과하여 들어왔었던 기록을 Stateful Flow Table에 기록(방명록)
* **Stateful Flow Table을 참조**하여 패킷 진입을 허용할지 차단할지 결정
* 패킷 필터링의 경우 들어오는 방향에 대한 패킷의 접근 제어 + 나가는 방향에 대한 패킷의 접근 제어 둘 다 필요하지만 Stateful Inspection은 들어오고 나가는 패킷에 대해 동적으로 접근 제어   
<img width="699" alt="스크린샷 2021-05-21 오후 12 30 31" src="https://user-images.githubusercontent.com/57285121/119078021-5740e780-ba30-11eb-8fda-017a55cf58dd.png">   

* 장점   
> * 들어오고 나가는 패킷에 대해 일일이 접근 제어를 하지 않고 동적으로 패킷의 접근 제어가 가능함(Stateful Flow Table을 이용해서)   
* 단점   
> * 방화벽을 종료하고 재시작 할 경우 Stateful Flow Table의 정보가 손실될 수 있어서 정상적인 패킷도 거부가 발생할 수 있음   

# WAF(Web Appliaction Firewall)
* 웹 방화벽
* 웹의 비정상 트래픽을 탐지하고 차단하기 위한 방화벽
* 기존 방화벽은 TCP/IP 헤더를 기반으로 접근 규칙을 설정함(Stateless & Stateful)
* WAF는 Application Payload(URI 등)까지 확인하여 접근 규칙 설정
* 웹 서버쪽으로 전송되는 Inbound의 HTTP Request 패킷을 확인하여 악의적인 정보를 전송하지 못하게 함(비정상적인 접근을 제한)
* 웹 서버에서 외부로 응답하는 Outbound의 HTTP Response 패킷을 확인하여 특정 정보의 유출을 막음

## Whitelist 
   
<img width="507" alt="스크린샷 2021-05-25 오후 2 20 09" src="https://user-images.githubusercontent.com/57285121/119443286-51b30c80-bd64-11eb-9236-722cd3524ed3.png">
   
* Positive rule
* Whitelist에 허용할 URI를 등록하여 등록되지 않은 URI를 요청할 시 요청 거부
* 관리자가 직접 허용할 패턴에 대해 직접 지정(잘못된 입력값은 다 차단)

## Blacklist
   
<img width="507" alt="스크린샷 2021-05-25 오후 2 20 38" src="https://user-images.githubusercontent.com/57285121/119443313-62638280-bd64-11eb-9a44-0e365d2f6e61.png">
   
* Negative rule
* Blacklist에는 URI를 확인하여 외부로부터 악의적인 공격 패턴을 검출하고 차단
* 특정 악성 바이러스코드 혹은 공격에 대해 차단 가능
## 1세대 WAF
   
<img width="391" alt="스크린샷 2021-05-25 오후 1 42 47" src="https://user-images.githubusercontent.com/57285121/119440352-18c46900-bd5f-11eb-920c-a5fbd07f533e.png">
   
* Whitelist, Blacklist 병행
* 자동으로 Blacklist 온라인 업데이트 진행
* 관리자가 Whitelist 직접 생성 및 관리해야함(관리자의 부담 상승)
* 공격 유형이 다양해짐에 따라 등록해야 할 항목들이 많아짐

## 2세대 WAF
   
<img width="397" alt="스크린샷 2021-05-25 오후 1 44 12" src="https://user-images.githubusercontent.com/57285121/119440446-4c06f800-bd5f-11eb-89a0-1c0aefd087e6.png">
   
* 보호받아야 할 웹 애플리케이션을 일정 기간동안 모니터링하여 분석한 후 Whitelist를 자동으로 생성
* 다양한 공격 유형을 파악하지 못할수도 있음(오탐 가능성)
* Whitelist를 자동으로 생성하긴 하지만 잘못된 Whitelist가 생성될 수 있기 때문에 관리자의 검토 및 관리가 필요(여전히 관리자의 부담 존재)

## 3세대 WAF
   
<img width="437" alt="스크린샷 2021-05-25 오후 1 57 19" src="https://user-images.githubusercontent.com/57285121/119441466-211da380-bd61-11eb-96ea-b0f104d5c869.png">
   
* 지능형 웹방화벽
* 공격 유형별 Blacklist, Whitelist 생성을 위한 URI 등의 트래픽 분석 기법을 논리적으로 결합
* 공격 패턴을 분석하여 침입을 인식하는 논리적인 패턴을 생성하여 외부 공격으로부터 보호
* 최소한의 패턴 추가만으로 오탐을 최소화함
* 관리자의 리스트 관리(검토) 부담이 줄어들고 공격 유형별 정책 관리에 집중이 가능

# 방화벽 구조
## Screening Router   
<img width="510" alt="스크린샷 2021-05-20 오후 11 29 55" src="https://user-images.githubusercontent.com/57285121/118997110-5c1b8200-b9c3-11eb-927f-0830dae81589.png">   

* 내부 네트워크와 외부 네트워크 사이에 **패킷필터링**을 적용한 라우터를 통해 방화벽을 구축
* TCP/IP 헤더에 대해서 접근제어(패킷 필터링)
* 장점   
> * 저렴한 가격으로 방화벽 구축 가능   
* 단점   
> * 세부적인 보안정책을 적용하기가 어려움(특히 4계층 이상)   
> * ACL의 항목이 많아질 수록 트래픽 과부하 가능성   
> * 접속 실패에 대한 로그 지원X   

## Bastion Host
   
<img width="574" alt="스크린샷 2021-05-25 오후 3 10 25" src="https://user-images.githubusercontent.com/57285121/119447790-5fb85b80-bd6b-11eb-87ce-8b86aedea3c6.png">
   
* 침입 차단 소프트웨어가 설치되어 Untrusted Zone과 Trusted Zone 사이에서 연결점 역할을 수행하는 호스트
* Untrusted Zone에서 Trusted Zone에 접근하기 위해서는 반드시 Bastion Host를 거쳐야함
* Bastion Host는 외부에 유출되어 있기 때문에 Bastion Host에는 중요한 정보(사용자 계정 정보 등)를 포함시키지 않음
* Proxy Server의 역할 
* SSH를 통해 사용자 인증
* 로깅을 통해 모니터링
* 장점   
> * Screening Router보다 강력한 접근 제어   
> * 로깅 기능 제공   
* 단점   
> * Bastion Host가 고장나게 되면 모든 트래픽을 허용하게 되어 보안이 취약해질 수 있음   

## Dual-Homed Gateway   
<img width="501" alt="스크린샷 2021-05-21 오전 12 05 47" src="https://user-images.githubusercontent.com/57285121/119002975-4eb4c680-b9c8-11eb-97de-24c32cd20570.png">   

* NIC가 두 개 이상 갖춰진 Bastion Host
* 하나는 내부 네트워크, 하나는 외부 인터넷으로 연결(물리적 구분)
* 라우팅 기능이 없기 때문에 내부 네트워크와 외부 인터넷의 직접적인 통신이 불가
* 장점   
> * 네트워크가 물리적으로 구분되어 있기 때문에 Bastion Host보다 트래픽 관리가 효율적   
* 단점   
> * Bastion Host에 대한 로그인 정보 유출 시 네트워크 보호가 불가능   

## Screened Host Gateway   
<img width="595" alt="스크린샷 2021-05-21 오후 12 15 28" src="https://user-images.githubusercontent.com/57285121/119076836-3d060a00-ba2e-11eb-8021-9aa612beb034.png">   

<img width="860" alt="스크린샷 2021-05-21 오후 12 24 46" src="https://user-images.githubusercontent.com/57285121/119077597-899e1500-ba2f-11eb-83b6-b1a2894c67bd.png">   

* Screening Router와 Single/Dual-Homed Gateway를 조합해서 사용하는 방법
* 패킷 필터링으로 1차 방어 + Bastion Host의 프록시 등을 통해 2차 방어
* Screening Router로 3계층, 4계층 접근제어 + Bastion Host로 7계층 접근 제어
* 장점   
> * 두 번에 걸친 접근제어를 통한 강력한 접근 제어   
* 단점   
> * 구축 비용이 비쌈   

