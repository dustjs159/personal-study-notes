OSI 7 Layer
====================================
## Summary
- Last Updated : 21.06.28 Mon   
- Updated by : 윤연선
-----------------------------------

# OSI 7 Layer
* OSI(Open System Interconnection, 개방형 시스템 간 상호 접속)
* 다른 시스템 간 원활한 통신을 위해 ISO(국제 표준화 기구)에서 제안한 통신 규약**(Protocol)**
* 네트워크가 통신하는 구조를 계층으로 구분하여 각 계층간 상호 작동하는 방식을 정해놓은 규약
* 서로 다른 컴퓨터 간 원활한 데이터 통신이 목적
* 1~4 계층(하위 계층) : 주요 통신 기능 구현 / 5~7 계층(상위 계층) : 애플리케이션 기능 구현
* OSI 각 계층별 데이터들을 PDU(Process Data Unit)이라고 하고, PDU는 각 계층별로 이름이 다름
* 문제 해결(트러블 슈팅)을 위해 알아야 할 주요 개념
   
![osi1](https://user-images.githubusercontent.com/57285121/115154807-b28d5c00-a0b7-11eb-833d-ba61fac04bf2.png)
   
# 1 계층 : 물리 계층(Physical Layer)
* 데이터 전송을 위한 물리적 연결을 담당
* 물리적 매체를 정의(랜선, 동출케이블 등)
* 데이터를 전기적 특성(ON/OFF, 0 or 1)을 이용하여 물리적 매체를 통해 전송할 수 있도록 함
* 데이터 전송 단위 : 비트(bit)
* 사용되는 네트워크 장비 : 리피터, 허브 

# 2 계층 : 데이터 링크 계층(Data Link Layer)
* 근접한 시스템 간에 신뢰성 있는 데이터를 전송
* **MAC주소**를 기반으로 목적지에 데이터를 전송
* 흐름제어(Flow contorl) : 송신측에서 수신측의 처리속도를 고려하여 데이터를 전송
* 프레임동기화(Framing) : 비트들을 Frame이라는 논리적 단위로 변환
* 오류제어(Error control) : Framing과정에서 발생하는 오류들을 검출하고 오류 발생 시 재전송 요청
* 데이터 전송 단위 : 프레임(Frame)
* 사용되는 네트워크 장비 : 랜카드, 브리지, **스위치**
* 프로토콜 : Ethernet

# 3 계층 :  네트워크 계층(Network Layer)
* 시스템 간의 네트워크 연결을 설정, 유지, 해제
* IP 주소를 기반으로 네트워크 상 호스트에게 데이터를 전송
* 데이터 전송 단위 : 패킷(Packet)
* 프로토콜 : IP, ARP, RARP, IPsec, ICMP 

# 4 계층 : 전송 계층(Transport Layer)
* 송, 수신측 간 신뢰성 있는 데이터 전송을 담당 
* 데이터 전송 단위 : 세그먼트(Segment)
 

# 5 계층 : 세션 계층(Session Layer)
* 세션의 수립과 해제

# 6 계층 : 표현 계층(Presentation Layer)
* 데이터를 이해할 수 있는 형식에 맞게 변환 

# 7 계층 :  응용 계층(Application Layer)
* 애플리케이션별 서비스 제공
* 데이터 전송 단위 : 데이터(Data), 메시지(Message)
* 프로토콜 : HTTP, FTP, SSH 
