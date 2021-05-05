VXLAN
=============================================

# Network Overlay
* 실제 물리적인 네트워크 위에 가상의 네트워크를 구축하는 기술   
* 오버레이 네트워크의 노드들은 논리적인 링크로 연결될 수 있으며 논리적 링크는 고려하지 않음
<img width="529" alt="스크린샷 2021-05-04 오후 5 20 04" src="https://user-images.githubusercontent.com/57285121/116977117-037a9280-acfd-11eb-87f0-f2db6c3522cc.png">   

# VXLAN(Virtual eXtensible Local Area Network)
* VXLAN은 Overlay 네트워크 구축을 위한 프로토콜 중 하나   
<img width="663" alt="스크린샷 2021-05-04 오후 5 24 49" src="https://user-images.githubusercontent.com/57285121/116977642-a501e400-acfd-11eb-8f98-27c0c45fea5c.png">   

* VXLAN은 터널링 기반 기술   
> * 터널링(Tunneling) : 데이터를 네트워크 상에서 가상의 파이프를 통해 전달시키는 기술   
* 가상의 네트워크에서 발생한 패킷은 캡슐화(Encapsulation)되어 물리 네트워크를 통고화고 다시 캡슐화 해제(Decapsulation)되어 가상 네트워크로 전달
* VTEP(VXALN Tunnel Ent Point)는 패킷의 캡슐화와 해제가 발생하는 지점. 가상의 SW 장치가 될 수도 있고, VXLAN을 지원하는 물리 장치가 될 수도 있음
* 캡슐화된 패킷은 VNI(VXLAN ID)를 통해 어느 가상 네트워크의 패킷인지 구분(VLAN의 VLAN ID 역할)
* *캡슐화된 패킷을 터널링 기술로 전달하고 해제*

# VXLAN Packet   
<img width="809" alt="스크린샷 2021-05-04 오후 6 44 14" src="https://user-images.githubusercontent.com/57285121/116986422-bbfa0380-ad08-11eb-9c13-57b7dfecd773.png">   



