VXLAN
=============================================


# VXLAN(Virtual eXtensible Local Area Network)
* L2 네트워크의 확장
* 기존 VLAN은 VLAN ID를 4096개 까지밖에 지정이 안된다는 한계가 있음
* 기존 네트워크 스위치는 MAC주소 테이블 수용에 한계가 있음
* 그래서 네트워크 스위치에 MAC주소 테이블을 전부 보관하는 것이 아닌 Virtual Switch를 통해 각자의 MAC주소 테이블을 보관함
* Virtual Switch(가상 스위치)   
> * 눈에 보이지 않는 스위치를 가상머신의 커널에 생성   
> * 게스트 OS에 일일이 NIC를 직접 할당하는것은 불가능   
> * 게스트 OS의 가상 스위치와 물리적인 NIC를 연결하여 사용   
<img width="212" alt="스크린샷 2021-05-07 오후 2 03 57" src="https://user-images.githubusercontent.com/57285121/117400191-15e30f00-af3d-11eb-96d2-c13dee993d56.png">   

* VXLAN은 Overlay 네트워크 구축을 위한 프로토콜 중 하나   
<img width="663" alt="스크린샷 2021-05-04 오후 5 24 49" src="https://user-images.githubusercontent.com/57285121/116977642-a501e400-acfd-11eb-8f98-27c0c45fea5c.png">   

* VXLAN은 **Tunneling** 기반 기술   
> * 터널링(Tunneling) : 데이터를 네트워크 상에서 가상의 파이프를 통해 전달시키는 기술   
* 가상의 네트워크에서 발생한 패킷은 캡슐화(Encapsulation)되어 물리 네트워크를 통고화고 다시 캡슐화 해제(Decapsulation)되어 가상 네트워크로 전달
* *캡슐화된 패킷을 터널링 기술로 전달하고 해제*
* **VTEP(VXALN Tunnel Ent Point)** : 패킷의 캡슐화와 해제가 발생하는 지점. 가상의 SW 장치가 될 수도 있고, VXLAN을 지원하는 물리 장치가 될 수도 있음   
* 각 VTEP은 물리 네트워크와 가상 네트워크를 연결하고 물리 네트워크의 IP 주소와 하나 이상의  VNI이 있음
* VTEP간 Control Plane(Routing) + 물리적 네트워크상 Data Plane(Forwarding)

# VXLAN Packet   
<img width="499" alt="스크린샷 2021-05-07 오후 2 13 44" src="https://user-images.githubusercontent.com/57285121/117400871-7292f980-af3e-11eb-824c-8f62f7b4097f.png">   

* MAC Over IP/UDP Header
* 물리적인 네트워크에서 패킷 전달을 위한 Outer MAC Header, Outer IP Header, Outer UDP Header
* VXLAN Header에는 어느 가상 네트워크의 패킷인지 구분하기 위한 **VNI(VXLAN ID)**(VLAN의 VLAN ID 역할)가 보관
* VNI는 24bit로 구성되어 있기 때문에 약 1600만개의 VNI 사용 가능
* VTEP은 캡슐화 진행 후 해당 패킷을 목적지 VTEP으로 전송

# VXLAN Broadcast & VTEP Mac Address Learning & Unicast  
<img width="858" alt="스크린샷 2021-05-07 오후 12 53 13" src="https://user-images.githubusercontent.com/57285121/117396218-79b50a00-af34-11eb-9109-2ce244786f7d.png">   

* 가상 네트워트에서 발생한 Broadcast 패킷을 물리 네트워크에서 Multicast 처리   
> * VXLAN은 Multicast기반 Flood & Learn   
* 가상 네트워크의 가상머신 A는 가상머신 B의 MAC 주소를 알기 위해 VTEP에게 ARP Request(Src MAC주소 + Src IP주소 + Outer Src IP주소)를 VLAN ID 1과 함께 전송
* VTEP 1은 가상머신 A가 보낸 가상 네트워크의 패킷을 확인하여 VLAN ID가 1인것을 확인 
* VTEP에는 VLAN 1과 VNI 10이 매핑되어있고 VNI 10은 IP Multicast 그룹에 참여되어 있는것을 확인
* VTEP은 VXLAN 패킷에 VNI 10을 포함하여 VXLAN 패킷으로 캡술화 한 후 IP Multicast 그룹의 IP 주소에 전송
* 해당 패킷은 IP Multicast 그룹에 참여하고 있던 VTEP 2, VTEP 3에 전송됨 
* VTEP은 패킷의 정보를 확인하여 Src MAC주소, Outer Src IP주소, VNI이 적힌 테이블을 생성하여 보관(VXLAN 패킷 캡술화 해제 전) 
* VTEP은 캡슐화 해제 후 ARP Request로 변환하여 가상머신 B, C에게 전송
* 목적지 IP B가 가상머신 B의 IP 주소이기 때문에 가상머신 B만 ARP Response를 가상머신 A에게 Unicast로 전송
* VTEP 2가 가지고 있던 Src MAC주소, VNI, Outer Src IP주소 테이블을 바탕으로 다시 VXLAN 패킷으로 캡슐화 하여 VTEP 1에 Unicast로 전송
* VTEP 1은 VXLAN 패킷을 수신하고 Src MAC주소, VNI, Outer Src IP주소 테이블을 생성하고 보관
* VTEP 1은 VXLAN 패킷을 캡슐화 해제하여 ARP Response로 변환하여 가상머신 A로 전송
* ***그 이후로는 각 VTEP이 가지고 있는 Src MAC주소, VNI, Outer Src IP주소 테이블을 바탕으로 Unicast통신을 함***

