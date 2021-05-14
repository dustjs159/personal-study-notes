Network Virtualization
===========================

# 네트워크 가상화
* 물리적으로 구현되어있는 네트워크(Underlay) 위에 여러 프로토콜을 운영하는 하나 이상의 논리적 네트워크(Overlay)를 구현하는 기술

# Underlay/Overlay   
<img width="410" alt="스크린샷 2021-05-15 오전 12 05 47" src="https://user-images.githubusercontent.com/57285121/118290358-529ca080-b511-11eb-98a7-b7d7d099b23d.png">   
## Underlay
* 물리적 네트워크
## Overlay 
* 논리적 네트워크
* **Tunneling**이 가장 중요한 기술
* 대략적 과정
1. 가상머신 A가 데이터를 송신
2. Hypervisor에 데이터 전달
3. Hypervisor가 데이터와 목적지 Hypervisor의 주소를 캡슐화
4. 캡슐화된 데이터를 물리 네트워크로 전송 
5. 데이터가 목적지 Hypervisor에 전달
6. 캡슐화된 데이터를 받은 Hypervisor가 캡슐화 해제
7. Hypervisor는 해제한 캡슐을 확인하여 목적지 가상머신에게 전송
8. 가상머신 B에게 데이터 전달

# 네트워크 가상화가 등장한 배경   
* 하드웨어 의존적인 인프라 구축은 많은 비용이 요구됨
* 기존 인프라 확장 시 Down시간으로 인한 고가용성 하락
* 기존 구축된 인프라에 변경사항의 도입이 어려움
* 빠르고 유연한 네트워크 인프라 구축이 필요하게 됨

# 구현 종류
## 라우터 가상화
* **VRF(Virtual Routing & Forwarding)**
* Layer 3 가상화   
* 스위치들을 묶은 라우터를 가상화하는 것이 아닌 라우터의 기능인 Routing을 가상화
* Routing Table : Routing 알고리즘을 통해 만들어진 테이블
* Forwarding Table : Routing Table을 참조하여 목적지의 주소가 기록된 테이블 
* 라우팅 테이블을 여러 개 만들어서 통신이 필요한 곳만 해당 라우팅 테이블을 참조하도록 하는 기술   
<img width="948" alt="스크린샷 2021-05-15 오전 5 56 03" src="https://user-images.githubusercontent.com/57285121/118330089-3d8c3580-b542-11eb-95ff-27a24c39bf9e.png">   

* 각각 라우팅 프로토콜을 다르게 적용해야함(호스트들을 나누든지, 프로세스별로 나누든지)
* 같은 라우팅 테이블을 참조하지 않는(VRF가 다른) 호스트와 통신을 하고싶을 때는 라우팅 테이블을 참조하기 전에 VRF 인터페이스를 거치지 않고 바로 해당 목적지로 전송

# 주요 구현 기술 
## NFV(Network Function Virtualization)
* 방화벽이나 로드밸런서 등의 기능을 전용 하드웨어로부터 분리하여 가상 서버로 그 기능을 제공하는 기술
* 하드웨어적인 부분을 소프트웨어적(가상 머신)으로 구현하여 가상 서버에서 실행
* 네트워크 기능을 가상화하여 서비스 제공자가 관리하는 형태


## SDN(Software Defined Network)
* 기존 네트워크 시스템의 서버 하드웨어 영역의 라우터와 스위치를 소프트웨어적으로 대체하는 기술
* Data Plane(트래픽 관리)   
> * 네트워크 계층에서 실제 패킷을 전송하는 역할(Forwarding)   
* Control Plane(네트워크 관리)   
> * 네트워크 계층에서 라우팅을 담당(Routing)   
* 기존 라우터가 Data Plane과 Control Plane이 묶여있었다면 **SDN은 Data Plane과 Control Plane을 분리**
* 라우터는 Data Plane의 패킷의 전송(Forwarding)만 담당하고 Control Plane의 라우팅은 중앙의 서버(**SDN Contorller**)가 담당


# Network Overlay
* 서비스의 인프라 규모가 커지면서 네트워크의 구성이 점점 복잡해짐
* 이러한 배경을 바탕으로 실제 물리적인 네트워크 위에 가상의 네트워크를 구축하는 기술을 통해 네트워크 구성의 복잡함을 해결   
* 오버레이 네트워크의 노드들은 논리적인 링크로 연결될 수 있으며 논리적 링크는 고려하지 않음
<img width="529" alt="스크린샷 2021-05-04 오후 5 20 04" src="https://user-images.githubusercontent.com/57285121/116977117-037a9280-acfd-11eb-87f0-f2db6c3522cc.png">   

# Hypervisor
