VNetwork
===========================
네트워크 가상화
---------------------------

# 네트워크 가상화   
* 네트워크를 논리적으로 분할하여 기존 네트워크에 논리적인 구역을 만듦
* 물리적 네트워크 상의 두 지점을 물리적으로 연결하는 것이 아닌 논리적인 터널을 만들어 두 지점을 연결


# Network Overlay
* 서비스의 인프라 규모가 커지면서 네트워크의 구성이 점점 복잡해짐
* 이러한 배경을 바탕으로 실제 물리적인 네트워크 위에 가상의 네트워크를 구축하는 기술을 통해 네트워크 구성의 복잡함을 해결   
* 오버레이 네트워크의 노드들은 논리적인 링크로 연결될 수 있으며 논리적 링크는 고려하지 않음
<img width="529" alt="스크린샷 2021-05-04 오후 5 20 04" src="https://user-images.githubusercontent.com/57285121/116977117-037a9280-acfd-11eb-87f0-f2db6c3522cc.png">   

# NFV(Network Function Virtualization)
* 방화벽이나 로드밸런서 등의 기능을 전용 하드웨어로부터 분리하여 가상 서버로 그 기능을 제공하는 기술
* 하드웨어적인 부분을 소프트웨어적(가상 머신)으로 구현하여 가상 서버에서 실행
* 네트워크 기능을 가상화하여 서비스 제공자가 관리하는 형태


# SDN(Software Defined Network)
* 기존 네트워크 시스템의 서버 하드웨어 영역의 라우터와 스위치를 소프트웨어적으로 대체하는 기술
* Data Plane(트래픽 관리)   
> * 네트워크 계층에서 실제 패킷을 전송하는 역할(Forwarding)   
* Control Plane(네트워크 관리)   
> * 네트워크 계층에서 라우팅을 담당(Routing)   
* 기존 라우터가 Data Plane과 Control Plane이 묶여있었다면 **SDN은 Data Plane과 Control Plane을 분리**
*  라우터는 Data Plane의 패킷의 전송(Forwarding)만 담당하고 Control Plane의 라우팅은 중앙의 서버(**SDN Contorller**)가 담당

# Hypervisor
