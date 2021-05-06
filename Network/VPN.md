VPN
=========================

# VPN(Virtual Private Network)
* 가상 사설망
* 공용 망을 이용하여 사설 망을 사용하며 조직 내 인원들(회사 내부 직원 등)만 사용할 수 있게 네트워크를 구성하는 방법
* LAN과 LAN을 연결하는 WAN구성 시 거리가 너무 멀어질수록 많은 비용이 발생
* ISP들이 제공하는 공용 망(인터넷)을 이용하여 구축이 가능하기 때문에 기존의 사설망을 구축하는데 드는 비용이 줄어듦
* 공용 망으로 기업들의 업무 자료들을 보내기에는 보안성이 떨어진다는 단점이 존재
* VPN은 이러한 보안성이 떨어진다는 문제를 해결하기 위해 별도의 장비를 통해 트래픽을 암호화, 복호화 진행   
<img width="735" alt="스크린샷 2021-05-05 오전 2 01 16" src="https://user-images.githubusercontent.com/57285121/117041346-d1d9e980-ad45-11eb-8c9c-edd33e2f4f7a.png">   

* VPN 네트워크에 접속하게 되면 외부에 있는(사설 망에 포함되지 않은) 컴퓨터라도 내부 네트워크에 접속해 있는 것 처럼 사용 가능
* 사설 망에 속하지 않은 호스트가 내부 네트워크의 VPN에 접속하게 되면 사설 망의 IP 대역에 속하는 것 처럼 보이게 됨
* VPN 구현 기술 : **Tunneling**,  **암호화** , **인증**
* VPN 구성 유형
> * Site to Site VPN : 본사(LAN)와 지사(LAN)을 VPN 장비를 통해 연결   
> * Site to Client VPN : LAN에 호스트가 VPN 클라이언트 프로그램을 이용하여 접속   
* VPN 장점
> * 거리에 상관 없이 사설 망 이용 가능   
> * 터널링, 암호화 기법을 이용한 보안성   
> * 구축 비용 절감   
* VPN 단점
> * 일반적인 사설 망보다는 속도가 느림   
> * 명확한 표준이 없어서 ISP마다 다른기술을 사용하다 보니 서로 다른 ISP 간 연동에 문제가 발생
   
<img width="853" alt="스크린샷 2021-05-06 오후 2 50 22" src="https://user-images.githubusercontent.com/57285121/117248136-68a7c280-ae7a-11eb-965c-861aa572e6b5.png">
   
# Tunneling
* VPN 내 호스트 간 가상의 경로(터널)을 설정하여 그 터널을 통해 캡슐화된 데이터를 전송하는 기술
* 공용 망에서 사설 망과 같은 보안효과를 주기 위함
* 터널링으로 전송되는 데이터를 Payload라고 함
* 2계층 터널링은 주로 L2C에 사용되고 3계층 터널링은 주로 L2L에 사용됨
* 터널링 프로토콜은 사설 망의 패킷이 공중 망 위에서 안전하게 송, 수신 될 수 있도록 라우팅 정보와 데이터를 캡슐화. 캡슐화된 패킷은 라우팅 정보를 확인하여 터널의 목적지로 전송되고 목적지에 도착 시 캡슐화를 해제하여 최종 목적지로 전송됨    
<img width="501" alt="스크린샷 2021-05-06 오후 3 44 31" src="https://user-images.githubusercontent.com/57285121/117253231-f509b380-ae81-11eb-89ed-c3946f608a13.png">   
POP : ISP에서 제공하는 인터넷(공용 망)에 접근하기 위한 접점   

* 터널링 지원 프로토콜 : VPN 노드간 통신하는 패킷 암호화 + 터널 생성 관리 + 암호화   
> * PPTP(Point to Point Protocol)   
> * L2F(Layer 2 Forwarding)   
> * L2TP(Layer 2 Tunneling Protocol)   
> * IPsec(IP Security) VPN   
> * MPLS
> * SSL VPN

# PPTP(Point to Point Tunneling Protocol)
* PPP(Point to Point Protocol) : 점 대 점 데이터 링크 프로토콜
* 데이터 링크 계층에서 사용
* 주요 구성 요소 : LCP, NCP
* LCP(Link Control Protocol)   
> * PPP 링크를 개설, 유지, 종료를 담당하는 회선관리용 프로토콜      
* LCP의 인증용 프로토콜 PAP, CHAP
> * PAP(Password Authentication Protocol) : 2 way-handshake를 통한 사용자 인증   
<img width="461" alt="스크린샷 2021-05-06 오후 10 52 08" src="https://user-images.githubusercontent.com/57285121/117309771-b2fe6300-aebd-11eb-8cb2-b7dfb0e82eb4.png">   

> * CHAP(Challenge Handshake Authentication Protocol) : PAP보다 보안이 강화된 3 way-handshake를 통한 사용자 인증   
<img width="488" alt="스크린샷 2021-05-06 오후 10 54 10" src="https://user-images.githubusercontent.com/57285121/117310132-fb1d8580-aebd-11eb-8ed2-c4b99afc157e.png">   

> > * 사용자는 서버로부터 온 challenge 패킷을 해시함수를 적용하여 다시 서버에게 전송. 서버는 일치 여부를 확인하고 인증을 진행

* NCP(Network Control Protocol)
> * 다양한 네트워크 계층의 프로토콜들을 제어
<img width="419" alt="스크린샷 2021-05-06 오후 3 22 27" src="https://user-images.githubusercontent.com/57285121/117250921-e53ca000-ae7e-11eb-914d-27c328497351.png">   

* 2계층 터널링. Site to Site VPN.
* 클라이언트/서버 모델
* 클라이언트와 서버가 인증 절차를 거친 후에 터널링이 시작
* 터널을 통과하는 데이터를 캡슐화하여 전송
* PPP의 패킷을 IP 패킷으로 캡슐화 하여 IP 네트워크에서 전송 가능
* 컴퓨터와 컴퓨터가 유니캐스트 방식으로 데이터를 전송하여 외부로부터 보안을 유지
* TCP/IP를 그대로 이용하며 외부인의 접근을 차단하여 별도의 VPN을 운영
* 장점
> * 설치가 쉽고 구현을 위한 부하가 적다   
> * 통신 속도가 빠르다   
> * 거의 모든 OS에서 지원함
* 단점
> * 보안에 있어서 취약점이 있음


# L2TP(Layer 2 Tunneling Protocol)
* PPTP + L2F(Layer 2 Forwarding)
* UDP를 사용
* PPTP와 같이 PPP트래픽을 암호화 하기 때문에 IP, IPX, NetBEUI등 여러 프로토콜을 사용할 수 있음
* 두 지점간 여러 터널을 사용할 수 있음
* PPTP와 캡슐화 방식은 동일하지만 IPsec의 ESP를 도입하여 보안기능 제공   
<img width="472" alt="스크린샷 2021-05-06 오후 3 59 47" src="https://user-images.githubusercontent.com/57285121/117254995-179ccc00-ae84-11eb-86e9-572902a88bbe.png">   


# IPsec VPN
* IPsec : IP 기반 통신에 있어서 보안을 위한 프로토콜   
* IPsec의 동작모드 : 전송모드 / 터널모드
* 전송모드   
<img width="493" alt="스크린샷 2021-05-06 오후 9 16 09" src="https://user-images.githubusercontent.com/57285121/117296673-4a5cb980-aeb0-11eb-8d33-b6b97b4831af.png">   
> * IP 패킷의 페이로드를 보호하는 모드. 즉 IP보다 상위 계층의 프로토콜의 데이터들을 보호   
> * 상위 계층의 프로토콜만 보호하기 때문에 목적지 IP 주소와 출발지 IP 주소는 그대로 노출이 됨   
> * 
* IP계층에서 안전한 데이터 송,수신을 위한 3계층 터널링 프로토콜
* AH(Authentication Header), ESP(Encapsulation Security)를 통해 데이터 인중, 무결성, 기밀성 제공(보안 3요소) 
* IP헤더 + 페이로드로 이루어진 패킷이 터널 안으로 들어가면서 AH가 추가되어 캡슐화가 이루어지고 ESP헤더가 붙으면서 패킷을 암호화


# 암호화 및 인증
* 사설 망의 패킷이 공용 망을 지나다니기 위해서는 해당 패킷을 보안처리해야 함
