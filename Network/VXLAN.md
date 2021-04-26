VXLAN
=============================================
VXLAN(Virtual eXtensible Local Area Network)
---------------------------------------------

# Network Overlay
* 네트워크에 연결되어 있는 host의 수가 점차 증가하면서 네트워크의 구성이 복잡해짐
* 이렇게 복잡한 네트워크 구성의 어려움을 해결하기 위해 구축한 가상의 네트워크(Network Overlay)
* 물리 네트워크 위에 별도로 가상의 네트워크를 구성하는 기술
* Overlay Network로 구성된 망 안의 노드들은 가상의 논리적인 경로로 연결될 수 있으며 각 경로들은 물리적 경로는 고려하지 않음. Ex) P2P 네트워크
* P2P 네트워크 (Peer-to-Peer Network)
> * 컴퓨터 간 양방향 데이터 통신   
> * 각 노드들이 트래픽과 자원을 할당해 부하를 분산   
* 비유하자면, 서울에서 부산까지 가는데 차로 이동을 하면 고속도로를 타고 톨게이트를 거치고 하는 복잡한 과정이 있는데 비행기를 타면 한방에 빠르게 도착이 가능   
![vxlan1](https://user-images.githubusercontent.com/57285121/115848065-731b9280-a45e-11eb-8322-cb96c2695dde.PNG)   
* 여러가지 문제점이 있음


# VXLAN
* VXLAN Header + UDP + IP 기반 전송
* VXLAN Header는 24bit VXLAN Network ID로 구성
* VXLAN내 VM MAC 주소가 MAC Table에 없는(학습하지 못한) VM MAC은 IP Multicast를 이용하여 목적지 VM MAC 주소가 있는 스위치에 전송
![vxlan2](https://user-images.githubusercontent.com/57285121/116047428-09de8e00-a6af-11eb-80c3-b9e735f28ebb.PNG)   
* IP Network만 연결되어 있고 VXLAN 기술로 구현된 네트워크 상의 vSwitch(Virtual Switch)


* 문제점
> 1. Network Overlay는 MAC 주소 기반으로 구현(L2 Switch를 사용)하는데 이에 따른 MAC 주소 테이블의 한계   
> 2. 가상의 네트워크 망에서 16Bit VLAN ID에서 최대 수용 가능한 VLAN 숫자의 한계   
> 3. 가상 네트워크망에서 이동성 한계   

* 비구조화 오버레이
> * 각 노드가 인접 노드를 선택할 때 제약이 없도록 설계   
> * 노드 탐색시 메시지를 인접노드에 차례로 전파해 확산   
> * 탐색 시 요청데이터에 맞는 정보를 찾아가는 유연한 탐색이 가능   
> * 노드가 너무 많아질 경우에는 탐색 시 속도 저하 가능성이 있고 메시지가 목적지까지 도달하지 못할 가능성이 있음   

* 구조화 오버레이
> * 노드 별 연결을 할 때 연결 대상이 미리 결정되어 있음   
> * 토폴로지가 정해져 있기 때문에 메시지가 목적지까지 도달하지 못하는 경우가 적음   

