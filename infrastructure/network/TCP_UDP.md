💻 [Network] TCP & UDP
=============

# 💡 TCP & UDP 
* OSI 7 Layers 중 전송(Transport) 계층에서 사용되는 프로토콜
* 데이터 전송 단위 : Segment

## 📌 TCP(Transmission Control Protocol)
* End-to-End간 신뢰성 있는 데이터 통신을 지원하는 프로토콜
* 데이터를 전송함에 있어서 신뢰성 있는 전송이 주 목적
  * 송신자측에서 전송한 데이터가 손상 없이 그대로 보존된 채 수신자가 데이터를 수신할 수 있도록
* 응용 프로그램간 구별을 위해 ``Port`` 번호 사용
* 연결형 서비스, 가상회선 방식
* 데이터의 순차전송을 보장
* 흐름제어, 혼잡제어, 오류제어 기능 지원

### ✔️ TCP Packet 구조

<img width="667" alt="스크린샷 2021-05-18 오전 12 50 29" src="https://user-images.githubusercontent.com/57285121/118518401-0d77a900-b773-11eb-8fab-dd6ee36ea2a8.png">   

* **Source Port** : 출발지 Port 번호
* **Destination Port** : 목적지 Port 번호
* Sequence Number : 순서 번호
* Acknowledgement Number : 확인 응답 번호
* Data offset : TCP header 길이 값
* Reserved : 예약값
* **Window** : 윈도우 크기
* Checksum : 오류검출
* Urgent Pointer(긴급 포인터) : 긴급 데이터 처리

### ✔️ TCP 통신 과정 : 3 Way-Handshake & 4 Way-Handshake
* 3 Way-Handshake : 데이터를 전송하기 전 정확한 전송을 위해 Client와 Server간 연결(세션)을 수립하는 과정

![tcp1](https://user-images.githubusercontent.com/57285121/116592013-75985380-a95a-11eb-9fc6-39aaf1a1281c.png)   

1. Client는 Server에 연결 요청을 위해 `SYN(Synchronization)` 패킷 전송   
2. Server는 LISTEN 상태에서 `SYN`을 받고 SYN_RCV 상태로 바뀌면서 Client의 연결 요청을 정상적으로 받았다는 의미로 `ACK(Acknowledgment)` 와 Client도 포트를 열어달라는 `SYN` 을 함께 전송
3. Client는 Server의 `ACK`와 `SYN`을 받고(이 때 `ACK`가 도착하지 않았다면 다시 Server에 `SYN`을 보냄)ESTABLISHED 상태가 되며 Server의 요청을 정상적으로 받았다는 의미로 `ACK`를 전송
4. Server는 `ACK`를 받고 ESTABLISHED 상태로 변경
5. Client/Server 둘 다 ESTABLISHED 상태가 되면 데이터 송, 수신 가능.  

* 4 Way-Handshake : 데이터 송, 수신이 모두 종료된 후 Client와 Server간 연결(세션)을 종료하는 과정

![tcp2](https://user-images.githubusercontent.com/57285121/116592385-e7709d00-a95a-11eb-88c3-a75103765837.png)

1. Client는 `FIN` 패킷 전송, Client는 FIN_WAIT_1 상태로 변경
2. Server는 CLOSE_WAIT 상태로 바뀌고 Client의 `FIN` 패킷을 잘 받았다는 `ACK` 를 Client에 전송 + 해당 포트의 Application 상태를 Close() 로 만듦   
3. Client가 `ACK` 를 성공적으로 받으면 FIN_WAIT_2 로 상태 변경  
4. Close()상태의 Application은 종료과정을 거치고 성공적으로 종료가 되었을 때 Client에게 `FIN` 패킷 전송 + Server의 상태를 LAST_ACK로 변경.  
5. FIN_WAIT_2 상태이던 Client는 `FIN` 패킷을 받으면 TIME_WAIT 상태로 바뀌며 Server에게 `ACK` 패킷(TIME_WAIT)을 전송.  
6. 일정 시간이 지나면 TIME_WAIT 상태이던 Client가 종료되고 `ACK` 를 받은 서버도 종료됨.  

### ✔️ TCP 흐름제어(Flow Control)
* TCP가 데이터 전송에 있어서 신뢰성을 보장하기 위한 기능
* 송신측과 수신측 간의 데이터 처리 속도 차이에서 발생하는 문제점을 해결하기 위한 방법(속도 조절)
* 수신측 데이터 처리 속도가 송신측보다 빠르면 문제가 되지 않지만, 송신측이 더 빠를 경우 문제 발생
* 수신측의 저장공간을 넘어서는 양의 데이터 수신 시 손실 가능성
* 흐름제어 방법 : Stop and Wait, Sliding Window
* Stop and Wait   
![tcp3](https://user-images.githubusercontent.com/57285121/116593135-be044100-a95b-11eb-9c9c-654e8d2c3c8c.png)   
  * 매번 전송한 패킷에 대해 확인(ACK)을 해야만 다음 패킷을 전송하는 방법   
  * 간단한 구조이지만 하나씩만 주고 받기 때문에 비효율   
* Sliding Window
![tcp5](https://user-images.githubusercontent.com/57285121/116641797-6c35d800-a9a8-11eb-8dbe-54fa5520fe17.png) 
  * 3 Way-Handshake 과정에서 송신측이 수신측의 윈도우 크기(한 번에 수신할 수 있는 데이터 양)만큼 ACK 없이 패킷을 전송할 수 있게 동적으로 흐름 제어   
  

### ✔️ TCP 혼잡제어(Congestion Control)
* TCP가 데이터 전송에 있어서 신뢰성을 보장하기 위한 기능
* 송신측의 데이터가 한 공유기나 라우터에 몰릴 경우(혼잡) 데이터를 처리하기 힘들어지게 되면서 호스트는 계속 재전송을 하게되어 Overflow발생
* Overflow를 줄이기 위해 송신측이 데이터 전송속도를 강제로 줄임
* 송신측과 네트워크 간 데이터 처리 속도 차이에서 발생하는 문제점을 해결하기 위한 방법
* 흐름제어가 호스트와 호스트간 데이터 처리 속도 차이를 해결하기 위한 방법이라면 혼잡제어는 호스트와 네트워크 간 데이터 처리 속도 차이를 해결하기 위한 방법
* 혼잡 회피 방법 : AIMD / Slow Start
* AIMD(Addictive Increase / Multiplicative Decrease)
  * 합 증가 / 곱 감소   
  * 처음에 데이터를 하나씩 보내고 문제없이 도착했을 경우 윈도우 크기를 1씩 증가시키며 전송   
  * 전송 실패 시 윈도우 크기를 절반으로 감소   
  * 네트워크 대역이 남아 도는 상황에서도 윈도우 크기가 늘어나는 속도가 너무 느려서(1씩 증가) 네트워크의 모든 대역을 활용하여 제대로된 속도로 통신하기 까지 오래걸림   
* Slow Start
  * 윈도우 크기를 2배씩 증가시키는 방법   
  * 임계점(Threshold)을 설정하고 해당 임계점에 다다르면 윈도우 크기를 1씩만 증가시키고 혼잡이 감지되면 윈도우 크기를 1로 줄임   
  * 윈도우 크기가 늘어나는 속도가 AIMD에 비해 상대적으로 빠르기 때문에 제대로된 속도로 통신하기 까지 시간이 상대적으로 적게 걸린다   
* **혼잡 발생시 윈도우 크기를 줄이거나 증가시키며 혼잡을 회피하는 알고리즘**

### ✔️ TCP 오류제어(Error Contorl)
* TCP가 데이터 전송에 있어서 신뢰성을 보장하기 위한 기능
* 주로 재전송 기반 오류 제어(ARQ)를 사용
* ARQ(Automatic Repeat reQuest) : 에러 발생시 재전송을 요구하는 방식   
![tcp6](https://user-images.githubusercontent.com/57285121/116654714-b5942080-a9c4-11eb-9ea5-f4df990d8f2f.png)   
  * 송신측으로부터 2번이 와야하는데 2번이 안오고 3번이 왔을 때 2번을 다시 보내야한다고 알려줌(이 횟수가 3회 이상 넘어가면 에러로 판단)

### ✔️ TCP Keep-Alive
   
<img width="688" alt="스크린샷 2021-07-02 오후 4 19 59" src="https://user-images.githubusercontent.com/57285121/124236390-5af87b80-db51-11eb-949c-349bbba30a27.png">
   
* 3-way handshake를 통해 연결된 세션을 없애지 않고 계속 사용하는 방식
* 일정 시간이 지나면 연결된 세션이 살아있는지 확인하기 위해 연결을 유지하길 원하는 쪽에서 아주 작은 양의 패킷 전송(클라이언트, 서버 둘 중 하나라도 Keep-Alive를 사용하면 세션 유지 가능)
* 3-way handshake 과정에서 타이머 설정
* 서로 Keep-Alive 확인을 위한 작은 패킷(Payload가 없는 껍데기 ACK 패킷)을 주고 받은 후, 타이머의 값이 0이되면 다시 패킷을 전송하여 설정한 타이머 값으로 다시 조정
* 설정한 타이머의 값 주기로 종단 간 연결을 유지하는 것이 주 목적

## 📌 UDP(User Datagram Protocol)
* 비연결형 서비스, 데이터그램 방식을 사용하여 패킷을 교환
* 순차전송X, 흐름제어X, 혼잡제어X
* 최소한의 오류만 검출
* 통신을 위한 논리적인 경로를 연결하고 해제하는 과정이 없기 때문에 TCP에 비해 속도가 빠름
* 데이터 전송에 있어서 수신측이 올바르게 수신했는지에 대한 책임을 지지 않음(TCP에 비해 신뢰성이 낮음)
* 비교적 신뢰성이 중요하지 않은 데이터를 전송할 때 사용하는 프로토콜. e.g. 실시간 영상 스트리밍   

|프로토콜 종류|TCP|UDP|
|:----------:|:-------------:|:------:|
|연결 방식|연결형|비연결형|
|패킷 교환 방식|가상회선 방식|데이터그램 방식|
|전송 순서|순차 전송O|순차 전송X|
|수신 여부 확인|수신 여부 확인O|수신 여부 확인X|
|통신 방식|Unicast|Unicast,Multicast,Broadcast|
|신뢰성|높음|낮음|
|속도|느림|빠름|   
   
## 가상회선 방식 / 데이터그램 방식
* 가상회선 방식   
![tcp9](https://user-images.githubusercontent.com/57285121/116654337-e2940380-a9c3-11eb-9bd9-191e6bdcbb26.png)   
  * 데이터를 전송하기 전에 논리적으로 경로를 연결함(가상회선 연결형)   
  * 모든 패킷을 전송하면 가상회선 해제, 패킷들은 전송 순서대로 도착(순차전송)   
  * 각 라우터들은 논리적 연결 시 최초 한 번만 경로를 설정   
* 데이터그램 방식   
![tcp10](https://user-images.githubusercontent.com/57285121/116654437-1ec76400-a9c4-11eb-83ab-bbe749b67397.png)   
  * 데이터 전송 전 논리적 경로 설정X(비연결형)   
  * 독립적으로 패킷 전송   
  * 라우터들은 최적의 경로를 선택하여 패킷을 전송하고 데이터에서 분할된 패킷들은 각각 다른 경로로 전송될 수 있음   
  * 수신측에 도착한 패킷들의 순서가 다를 수도 있음(순차전송X)   
* 다랑의 데이터를 연속적으로 전송 : 가상회선 방식 선택
* 소량의 데이터를 일시적으로 전송 : 데이터그램 방식 선택

## 📌 Port
* 네트워크 서비스나 특정 프로세스(응용프로그램)를 식별하는 번호
* OSI 7 계층중 4계층(Transport)에서 사용됨
* IP 주소가 호스트를 찾기 위한 주소라면 포트번호는 그 호스트 안에서 프로그램들을 찾기 위한 수단
* IP 주소 하나 당 0~65535 까지의 포트번호 사용 가능
* Well Known Port : 유명한 서버, 특정 서버들이 사용하는 번호   

|포트번호|프로토콜|
|:----------:|:-------------:|
|20|FTP(경로설정)|
|21|FTP(데이터 전송)|
|22|SSH(Secure Shell Protocol)|
|23|Telnet|
|25|SMTP(Simple Mail Transfer Protocol)|
|53|DNS(Domain Name System)|
|80|HTTP(HyperText Transfer Protocol)|
|443|HTTPS(Secure)|

* Registerd Port : 기관이나 사업자들이 사용할 수 있도록 예약된 번호   

|포트번호|프로토콜|
|:----------:|:-------------:|
|3306|MySQL|
|8080|HTTP 대체|
