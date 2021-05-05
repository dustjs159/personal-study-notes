VPN
=========================

# VPN(Virtual Private Network)
* 가상 사설망
* 공용 망을 이용하여 사설 망을 사용하며 조직 내 인원들(회사 내부 직원 등)만 사용할 수 있게 네트워크를 구성하는 방법
* LAN과 LAN을 연결하는 WAN구성 시 거리가 너무 멀어질수록 많은 비용이 발생
* 공용 망으로 기업들의 업무 자료들을 보내기에는 보안성이 떨어진다는 단점이 존재
* VPN은 이러한 보안성이 떨어진다는 문제를 해결하기 위해 별도의 장비를 통해 트래픽을 암호화, 복호화 진행   
<img width="735" alt="스크린샷 2021-05-05 오전 2 01 16" src="https://user-images.githubusercontent.com/57285121/117041346-d1d9e980-ad45-11eb-8c9c-edd33e2f4f7a.png">   

* VPN 네트워크에 접속하게 되면 외부에 있는(사설 망에 포함되지 않은) 컴퓨터라도 내부 네트워크에 접속해 있는 것 처럼 사용 가능
* 사설 망에 속하지 않은 호스트가 내부 네트워크의 VPN에 접속하게 되면 사설 망의 IP 대역에 속하는 것 처럼 보이게 됨
* VPN 구현 기술 : Tunneling,  암호화, 인증
* VPN 구성 유형
> * L2L (LAN to LAN) : 본사(LAN)와 지사(LAN)을 VPN 장비를 통해 연결   
> * L2C (LAN to Client) : LAN에 호스트가 VPN 클라이언트 프로그램을 이용하여 접속   
* 장점
> * 거리에 상관 없이 사설 망 이용 가능   
> * 보안성   
> * 구축 비용 절감   
* 단점
> * 일반적인 사설 망보다는 속도가 느림 


# Tunneling
* VPN 내 호스트 간 가상의 경로(터널)을 설정하여 그 터널을 통해 캡슐화된 데이터를 전송하는 기술
* 공용 망에서 사설 망과 같은 보안효과를 주기 위함
* 터널링으로 전송되는 데이터를 Payload라고 함
* Tunneling 지원 프로토콜   
* 2계층 : L2C의 역할을 주로 수행
> * PPTP(Point to Point Tunneling Protocol)   
> * L2TP(Layer 2 Tunneling Protocol)   
> * L2F
* 3계층
> * IPsec VPN  
> * MPLS   
> * GRE   
* 4~7계층
> * SSL VPN

# PPTP(Point to Point Tunneling Protocol)
* 가장 오래된 표준 VPN 프로토콜
* 클라이언트/서버 모델
* PPP(Point to Point Protocol)을 확장
> * PPP : 두 노드간 직접적인 연결을 위해 사용되는 프로토콜
* 컴퓨터와 컴퓨터가 유니캐스트 방식으로 데이터를 전송하여 외부로부터 보안을 유지
* TCP/IP를 그대로 이용하며 외부인의 접근을 차단하여 별도의 VPN을 운영
* IP주소의 충돌을 피하기 위해 LAN의 IP주소와 원격지 VPN의 IP주소가 달라야 함


# 암호화 및 인증

# 접근 제어


