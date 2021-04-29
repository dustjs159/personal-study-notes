===========================================




# TCP(Transmission Control Protocol)
* End-to-End간 신뢰성 있는 데이터 통신을 지원하는 프로토콜
* 데이터를 전송함에 있어서 신뢰성있는 전송이 주 목적
* 연결형 서비스, 가상회선 방식
* 데이터의 순차전송을 보장
* 흐름제어, 혼잡제어, 오류제어 기능 지원
* 데이터를 전송할 때 마다 3 way-handshake를 통해 연결을 해야하므로 시간이 상대적으로 많이 소요됨

# 3 way-handshake / 4 way-handshake
* 3 way-handshake : 데이터를 전송하기 전 정확한 전송을 위해 송신측과 수신측의 연결(세션)을 수립하는 과정
* 연결을 위한 3 way-handshake
* 과정
> * 1. Client는 Server에 연결 요청을 위해 SYN패킷 전송   
> * 2. Server는 LISTEN 상태에서 SYN을 받고 SYN_RCV 상태로 바뀌면서 Client의 연결 요청을 정상적으로 받았다는 의미로 ACK와 Client도 포트를 열어달라는 SYN 을 함께 전송   > * 3. Client는 Server의 ACK와 SYN을 받고(이 때 ACK가 도착하지 않았다면 다시 Server에 SYN을 보냄)ESTABLISHED 상태가 되며 Server의 요청을 정상적으로 받았다는 의미로 ACK를 전송.  
> * 4. Server는 ACK를 받고 Server역시 ESTABLISHED 상태로 변경.  
> * 5. Client/Server 둘 다 ESTABLISHED 상태가 되면 데이터 송, 수신 가능.  

* 4 way-handshake : 데이터 송, 수신이 모두 종료된 후 송신측과 수신측간 연결(세션)을 종료하는 과정
* 과정
> * 1. Client는 FIN 패킷 전송, Client는 FIN_WAIT_1 상태로 변경.  
> * 2. Server는 CLOSE_WAIT상태로 바뀌고 Client의 FIN패킷을 잘 받았다는 ACK를 Client에 전송 + 해당 포트의 응용프로그램 상태를 Close()로 만듦   
> * 3. Client가 ACK를 성공적으로 받으면 FIN_WAIT_2로 상태 변경.  
> * 4. Close()상태의 응용프로그램은 종료과정을 거치고 성공적으로 종료가 되었을 때 Client에게 FIN패킷 전송 + Server의 상태를 LAST_ACK로 변경.  
> * 5. FIN_WAIT_2 상태이던 Client는 FIN패킷을 받으면 TIME_WAIT 상태로 바뀌며 Server에게 ACK패킷(TIME_WAIT)을 전송.  
> * 6. 일정 시간이 지나면 TIME_WAIT 상태이던 Client가 종료되고 ACK를 받은 서버도 종료됨.  

# 흐름제어(Flow Control)
* TCP가 데이터 전송에 있어서 신뢰성을 보장하기 위한 기능
* 송신측과 수신측 간의 데이터 처리 속도 차이에서 발생하는 문제점을 해결하기 위한 방법(속도 조절)
* 수신측 데이터 처리 속도가 송신측보다 빠르면 문제가 되지 않지만, 송신측이 더 빠를 경우 문제 발생
* 수신측의 저장공간을 넘어서는 양의 데이터 수신 시 손실 가능성
* Stop and Wait / Sliding Window


# 혼잡제어(Congestion Control)
* TCP가 데이터 전송에 있어서 신뢰성을 보장하기 위한 기능
* 송신측과 네트워크 간 데이터 처리 속도 차이에서 발생하는 문제점을 해결하기 위한 방법
* 흐름제어가 호스트와 호스트간 데이터 처리 속도 차이를 해결하기 위한 방법이라면 혼잡제어는 호스트와 네트워크 간 데이터 처리 속도 차이를 해결하기 위한 방법

# 오류제어(Error Contorl)
