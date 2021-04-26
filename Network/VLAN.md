VLAN
===============================

# LAN(Local Address Network)
* 근거리 통신망
* 학교, 회사, 가정 등 한 건물이나 일정한 지역 내에서 서로 다른 컴퓨터의 데이터 통신을 위해 묶은 네트워크 형태
* 동일한 IP 대역과 동일한 Subnet Mask를 사용하며 ARP(Address Resolution Protocol)가 닿는 범위   

# VLAN이 필요한 이유
* ARP프로토콜에서 ARP Request는 Broadcast방식으로 전송됨
* 네트워크 장비에 10대의 컴퓨터가 연결되어있다면 각각의 컴퓨터들이 다른 컴퓨터의 MAC주소를 알아내기 위해서는 최소 10번의 ARP Request 전송
* 네트워크 장비에 연결된 컴퓨터가 매우 많아질 경우 Broadcast의 양이 폭발적으로 증가하게 되고 그에 따라 컴퓨터들은 처리해야할 작업이 늘어나게 되어 데이터 전달 속도가 저하됨
* 라우터를 일일이 설치하여 각각 다른 IP대역을 갖도록해서 Broadcast되지 않도록 할 수 있지만 비용이 추가적으로 들어간다는 문제점이 발생   
이런 문제점들을 해결하기 위해 VLAN 구성이 필요   

# VLAN(Virtual LAN)
* Broadcast의 영역이 겹치지 않는 여러 개의 논리적인 LAN을 구성하는 기술   
* 하나의 물리적인 스위치를 VLAN을 사용해서 다수의 논리적인 LAN을 사용할 수 있음   
* 여러 개의 구별되는 Broadcast 영역을 만들기 위해 단일 2계층 네트워크를 분할하는데 이렇게 분할이 되면 패킷들은 하나 이상의 라우터들 사이에서만 이동이 가능하게 됨   
* VLAN을 지원하는 네트워크 장비는 VLAN을 다수 생성할 수 있고 이 VLAN을 통해 Broadcast 영역을 나눌 수 있음
* 이렇게 나누어진 VLAN들은 설정된 포트의 IP대역 안에서만 통신이 가능하고 다른 VLAN들과 통신을 하려면 L3 이상의 스위치나 라우터가 필요   
* VLAN은 1~4096의 번호를 붙여 서로 다른 VLAN들을 구분지을 수 있는데 이를 VLAN ID라고 함   
![vlan1](https://user-images.githubusercontent.com/57285121/116118745-98c3c880-a6f8-11eb-8801-822440a141b6.PNG)   
VLAN ID가 10인 PC1과 VLAN ID가 20인 PC2, PC3과는 통신 불가. PC2와 PC3은 VLAN ID가 같으므로 통신 가능   

# Trunk(Tagging)
* 만약에 VLAN이 폭발적으로 증가하게 된다면, 스위치의 포트 하나 하나에 일일이 VLAN을 구성하기가 힘들어짐(현실적으로 불가능)
* 트렁크는 스위치들 간에 프레임 전송 시에 하나의 포트에 다수의 VLAN이 지나갈 수 있도록 하는 기능   
* 서로 다른 스위치에 동일한 VLAN들이 존재할 경우에 주로 사용   
![vlan2](https://user-images.githubusercontent.com/57285121/116121751-e4c43c80-a6fb-11eb-9984-28e828208f60.PNG)   
* Trunk 설정이 완료된 스위치 내 포트들을 Trunk포트(그냥Trunk 설정이 안된 포트는 Access포트 라고함)라고 하며, 설정한 Trunk포트를 통해 위 그림처럼 VLAN1과 VLAN2이 통신이 가능  
> * (스위치 1의 VLAN1 > 스위치 1의 Access포트 > 스위치 1의 Trunk포트 > 스위치 2의 Trunk포트 > 스위치 2의 Access포트 > 스위치 2의 VLAN1)   
> * (스위치 1의 VLAN2 > 스위치 1의 Access포트 > 스위치 1의 Trunk포트 > 스위치 2의 Trunk포트 > 스위치 2의 Access포트 > 스위치 2의 VLAN2)   

# Tagging by IEEE 802.1Q
* 만약 한 스위치 내 하나의 포트에 여러 VLAN들의 프레임이 지나갈 때 해당 프레임이 어느 VLAN의 프레임인지 구별을 하기위한 방법 : 프레임에 Tag(VLAN의 정보)붙이기(Tagging)   
* IEEE 802.1Q : VLAN을 지원하는 트렁킹 프로토콜 중 하나
* 프레임들이 Trunk포트에 진입할 때 해당 프레임에 VLAN ID가 적힌 Tag를 프레임 내부에 끼워넣음(Tagging).   
* 다른 스위치에서는 프레임을 수신할 때 프레임에 붙은 Tag를 보고 VLAN ID를 확인   
* 프레임을 확장하는 방식   
![vlan3](https://user-images.githubusercontent.com/57285121/116127933-56ec4f80-a703-11eb-9f2a-9980b86e33df.PNG)   
IEEE 802.1Q 프로토콜을 이용하여 VLAN ID를 구별   

# VLAN 사용 목적
* 불필요한 브로드캐스트 트래픽 차단(과부하 감소)
* 네트워크 보안성 강화(다른 네트워크와 분리)
* 이중화

