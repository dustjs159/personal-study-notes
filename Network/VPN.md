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
> * L2TP(Layer 2 Tunneling Protocol)   
> * IPsec(IP Security) VPN   
> * SSL VPN

# PPTP(Point to Point Tunneling Protocol)
* PPP(Point to Point Protocol) : 점 대 점 데이터 링크 프로토콜
* 데이터 링크 계층에서 사용
* 주요 구성 요소 : 캡슐화(Encapsulation), LCP, NCP
* 캡슐화(Encapsulation)
> * 데이터 링크계층(2계층)에서 네트워크 계층(3계층) 데이터그램을 캡슐화   
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
> * 송, 수신측 간 서로 다른 프로토콜을 사용할 수 있도록 함   

* PPTP(Point to Point Protocol) : 2계층 터널링. Site to Site VPN.
* 클라이언트/서버 모델
* IP 기반의 네트워크만 지원하고 두 지점간 하나의 터널만 사용이 가능
* 클라이언트와 서버가 인증 절차를 거친 후에 터널링이 시작(LCP)
* 터널을 통과하는 데이터를 캡슐화하여 전송(Encapsualtion)
* PPP의 패킷을 IP 패킷으로 캡슐화 하여 IP 네트워크에서 전송 가능(NCP)

* GRE(Generic Routing Encapsulation)   
> * 공용 망의 라우터들은 사설 망 IP 주소로 라우팅을 할 수 없기 때문에 GRE 헤더를 붙이고 캡슐화 하여 라우팅이 가능하도록 함   
<img width="859" alt="스크린샷 2021-05-07 오전 12 12 05" src="https://user-images.githubusercontent.com/57285121/117322334-e09cd980-aec8-11eb-8ba8-a6c092f04ec0.png">   

> * GRE를 위한 20byte의 IP Header(출발지와 목적지의 공용 망 IP 주소) + GRE 관련 정보 4byte   

<img width="419" alt="스크린샷 2021-05-06 오후 3 22 27" src="https://user-images.githubusercontent.com/57285121/117250921-e53ca000-ae7e-11eb-914d-27c328497351.png">   
원래의 패킷(PPP 프레임)과 IP Header, GRE Header로 구성된 PPTP에서 전송되는 데이터.    

* 장점
> * 설치가 쉽고 구현을 위한 부하가 적다   
> * 통신 속도가 빠르다   
> * 거의 모든 OS에서 지원함
* 단점
> * 보안에 있어서 취약점이 있음   
> * PPP Payload를 암호화하는 과정에서 128비트 암호화를 진행하기 때문에 보안에 문제점이 있음


# L2TP(Layer 2 Tunneling Protocol)
* PPTP + L2F(Layer 2 Forwarding)
* UDP를 사용
* L2TP 자체에는 암호화 기능이 없기 때문에 IPsec와 결합하여 사용함
* 두 지점간 여러 터널을 사용할 수 있음
* PPTP와 캡슐화 방식은 동일하지만 IPsec의 ESP를 도입하여 보안기능 제공   
<img width="472" alt="스크린샷 2021-05-06 오후 3 59 47" src="https://user-images.githubusercontent.com/57285121/117254995-179ccc00-ae84-11eb-86e9-572902a88bbe.png">   


# IPsec VPN
* IP계층에서 안전한 데이터 송,수신을 위한 3계층 터널링 프로토콜
* 인증, 무결성, 기밀성 제공
* IPsec의 터널모드 이용
* AH(Authentication Header)
> * 인증/무결성은 보장되지만 암호화는 제공하지 않음   
* ESP(Encapsulation Security)
> * AH가 제공하지 않던 암호화까지 제공   
> * IP헤더 + 페이로드로 이루어진 패킷이 터널 안으로 들어가면서 ESP헤더가 붙으며 패킷을 암호화   
<img width="657" alt="스크린샷 2021-05-15 오전 2 24 20" src="https://user-images.githubusercontent.com/57285121/118306643-a9f83c00-b524-11eb-85b5-14e81646cbf7.png">   

## IKE(Internet Ket Exchange)
* 보안 관련 설정들(사용자 인증 방법, 암호화 방식 등)을 설정하고 관리하는 프로토콜
* IPsec의 AH는 송신자와 수신자가 같은 키를 공유하고 이 키로 해시를 돌려서 데이터의 일치 여부를 통해 인증을 진행
* IPsec의 ESP는 송신자와 수신자가 같은 키를 공유하고 대칭형 암호화 알고리즘을 통해 패킷을 암, 복호화를 진행
* 여기서 키를 어떻게 공유하는지, 암호화 알고리즘은 어떤 것을 사용하는지 등의 사전 협상
* 이러한 과정을 SA(Security Association, 보안 협상) 설정 절차라고 함
* IPsec VPN을 위한 선 처리 과정   
<img width="508" alt="스크린샷 2021-05-15 오전 2 41 50" src="https://user-images.githubusercontent.com/57285121/118308610-1bd18500-b527-11eb-8e6f-4027044860f3.png">   

* Phase 1, Phase 2 2단계로 진행

### Phase 1 (ISAKMP SA)
* 보안이 설정되지 않은 환경에서 보안이 설정된 터널을 만들기 위한 단계
* ISAKMP(Internet Security Assocation and Key Management Protocol)   
> * SA를 위한 절차 등을 정의한 프로토콜   
> * SA 항목 : 인증을 위한 키 공유, 암호화 알고리즘 협상 등

### Phase 2 (IPsec SA)
* 터널이 설정된 후 실제 데이터를 전송하기 위한 방법을 협상
> * Phase 1에서 설정된 SA를 바탕으로 실제 데이터 전송

# SSL VPN
* SSL을 이용해 애플리케이션 계층에서 클라이언트와 SSL VPN 장비간 통신에 대한 보안 제공
* 유동적인 IP를 사용하는 기기의 사용자가 내부로 접근할 때 유용
* IPsec VPN은 3계층에서만 적용이 가능하지만 SSL VPN은 4~7계층에서 모두 적용 가능
* 웹 브라우저 자체에서 지원
* Site to Site 보다는 Site to Client 에 더 적합
* IPsec VPN은 Site to Site를 위해 두 지점 다 IPsec VPN장비가 필요했지만 SSL VPN은 사용자가 외부 기기로 SSL VPN에 로그인하여 사용가능   
<img width="656" alt="스크린샷 2021-05-15 오전 4 27 03" src="https://user-images.githubusercontent.com/57285121/118319484-cea8df80-b535-11eb-9037-5b6614b79766.png">   
* 클라이언트는 SSL 장비에 로그인을 함(SSL 인증서 방식을 통해)
* 클라이언트가 SSL에 로그인이 성공한 후에 데이터 전송

<img width="479" alt="스크린샷 2021-05-15 오전 4 21 34" src="https://user-images.githubusercontent.com/57285121/118318943-0b280b80-b535-11eb-88f4-03a819aac515.png">   

<img width="662" alt="스크린샷 2021-05-15 오전 4 40 03" src="https://user-images.githubusercontent.com/57285121/118320745-a02c0400-b537-11eb-9afc-54eaef2a55af.png">   

* 로그인에 성공하면 **가상 IP**를 할당받고 내부 서버들에 접속이 가능
