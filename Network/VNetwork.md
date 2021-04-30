Network Virtualizaion
==============================
네트워크 가상화
------------------------------   

# 네트워크 가상화(Network Virtualization)
* 물리적인 네트워크를 하나 이상의 논리적인 네트워크로 세분화 하는 것처럼 보여지게 운영하는 기술
* 네트워크 인프라 자원 활용 극대화가 주된 목표

# 호스트 가상화
# 링크 가상화
# 라우터 가상화
# 스위치 가상화
# SDN(Software Defined Network)
# NFV(Network Function Virtualization) 

![vnet](https://user-images.githubusercontent.com/57285121/116063858-68603800-a6c0-11eb-8b18-22989b6b21fe.PNG)   

# Network Underlay
* 스위치와 라우터의 기능 모두 가상화

# Network Overlay
* 스위치의 기능만 가상화
* 물리적 스위치로 연결된 같은 네트워크 대역폭의 NIC를 하나로 묶어 vSwitch를 생성하여 관리하는 방식   
![vnet1](https://user-images.githubusercontent.com/57285121/116400223-c4fc5800-a864-11eb-98ed-b65186d78f8d.PNG)   
> * 여러 호스트들의 NIC를 하나의 스위치에서 관리할 수 있게되어 관리가 쉬워짐

* 네트워크에 연결되어 있는 host의 수가 점차 증가하면서 네트워크의 구성이 복잡해짐
* 이렇게 복잡한 네트워크 구성의 어려움을 해결하기 위해 구축한 가상의 네트워크(Network Overlay)
* 물리 네트워크 위에 별도로 가상의 네트워크를 구성하는 기술
* Overlay Network로 구성된 망 안의 노드들은 가상의 논리적인 경로로 연결될 수 있>으며 각 경로들은 물리적 경로는 고려하지 않음. Ex) P2P 네트워크
* P2P 네트워크 (Peer-to-Peer Network)
> * 컴퓨터 간 양방향 데이터 통신
> * 각 노드들이 트래픽과 자원을 할당해 부하를 분산
* 비유하자면, 서울에서 부산까지 가는데 차로 이동을 하면 고속도로를 타고 톨게이트
를 거치고 하는 복잡한 과정이 있는데 비행기를 타면 한방에 빠르게 도착이 가능
![vxlan1](https://user-images.githubusercontent.com/57285121/115848065-731b9280-a45e-11eb-8322-cb96c2695dde.PNG)
* 여러가지 문제점이 있음

# Network Overlay
* 네트워크에 연결되어 있는 host의 수가 점차 증가하면서 네트워크의 구성이 복잡해짐
* 이렇게 복잡한 네트워크 구성의 어려움을 해결하기 위해 구축한 가상의 네트워크(Network Overlay)
* 물리 네트워크 위에 별도로 가상의 네트워크를 구성하는 기술
* Network Overlay로 구성된 망 안의 노드들은 가상의 논리적인 경로로 연결될 수 있으며 각 경로들은 물리적 경로는 고려하지 않음. Ex) P2P 네트워크
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

