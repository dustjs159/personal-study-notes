ARP
=================================
## Summary
- Last Updated : 21.09.02 Thu   
- Updated by : 윤연선
-----------------------------------

# ARP(Address Resolution Protocol)
* 주소 결정 프로토콜
* 해당 목적지의 **IP 주소로 MAC 주소를 알아내기 위한 프로토콜 (IP Address > MAC Address)** 
* OSI 7 Layers 중 Layer 3 (Network Layer)에서 사용되는 프로토콜
* LAN(Local Area Network)에서 호스트 간 통신을 할 때는 IP 주소와 MAC 주소를 같이 이용하게 됩니다. 목적지의 IP 주소를 확인하여 해당 IP 주소에 맞는 MAC 주소를 가진 호스트에게 정확하게 전달하기 위함입니다.

# RARP(Reverse Address Resolution Protocol)
* 역순 주소 결정 프로토콜
* ARP와 반대로 **MAC 주소로 IP 주소를 알아내기 위한 프로토콜 (MAC Address > IP Address)**

# ARP 동작원리
1. 송신자는 목적지의 MAC주소를 알아내기 위해 ARP Request 패킷을 Broadcast로 전송(목적지의 MAC주소를 모르기 때문에) 
2. ARP Request 패킷에는 응답을 받기 위해 송신자의 주소가 포함됨
3. 모든 호스트와 라우터들은 ARP Request 패킷을 수신
4. 목적지에 해당하는 수신자는 자신의 MAC주소를 넣어 응답 패킷을 송신자에게 Unicast로 전송

# ARP 동작과정
   
![arp1](https://user-images.githubusercontent.com/57285121/116058962-54fe9e00-a6bb-11eb-871f-4de7edfc0474.PNG)
   
1. 송신자는 목적지 IP Address를 지정하여 패킷 송신   
2. IP 프로토콜이 ARP에게 송신자 MAC주소, 송신자 IP주소, 수신자 IP주소로 구성된 ARP Request 메시지 생성 요청   
3. 생성된 ARP Request가 Broadcast로 전송  
   
![apr2](https://user-images.githubusercontent.com/57285121/116060350-c3902b80-a6bc-11eb-972e-7b49728906eb.PNG)
   
4. Broadcast로 ARP Request를 수신한 호스트 중에서 목적지 IP Address가 일치하는 시스템은 자신의 MAC주소를 포함한 ARP Reply(응답 메시지)를 송신측에 전송   
5. 최초 송신측은 목적지의 IP Address에 대응하는 MAC주소 획득   

***ARP Request = Broadcast, ARP Reply = Unicast***
