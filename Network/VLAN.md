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

# VLAN PORT Mode
* VLAN이 설정되는 스위치의 포트의 동작 방식
* Access Port Mode   
<img width="359" alt="스크린샷 2021-05-10 오후 7 09 31" src="https://user-images.githubusercontent.com/57285121/117643348-43d98500-b1c3-11eb-9e07-fd2e0c585d6f.png">   

> * PC와 스위치간 연결일 때 Tag을 붙이지 않고 나감   
> * 하나의 호스트가 하나의 VLAN만 지원 가능   
> * Access Mode로 동작하는 포트에 VLAN ID 할당   
> * 프레임 전송 시 스위치에서 Tag를 제거   

* Trunk Port   
<img width="348" alt="스크린샷 2021-05-10 오후 8 54 58" src="https://user-images.githubusercontent.com/57285121/117655405-fd3f5700-b1d1-11eb-9428-7543d4e26b31.png">   

> * 스위치와 스위치간 연결일 때 Tag를 붙인 채로 나감   
> * VLAN ID가 포함된 Tag를 통해 여러 VLAN의 프레임들을 구별하여 전송 가능   
> * Tag를 통해 여러 VLAN의 프레임들을 수용할 수 있음   

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
* Tag의 크기는 4 bytes
* 다른 스위치에서는 프레임을 수신할 때 프레임에 붙은 Tag를 보고 VLAN ID를 확인   
* 프레임을 확장하는 방식   
![vlan3](https://user-images.githubusercontent.com/57285121/116127933-56ec4f80-a703-11eb-9f2a-9980b86e33df.PNG)   
IEEE 802.1Q 프로토콜을 이용하여 VLAN ID를 구별  

# Untagged VLAN 
* Untagged Frame : Tag를 달지 않은 프레임
* Access Port로 프레임 송, 수신
* 4 bytes의 Tag가 모든 프레임에 붙을 경우 속도 저하 가능성 존재
* Tag가 붙어있지 않는 프레임을 모두 VLAN 1(Default)로 처리
* Tag를 붙이고 분해하는 과정이 없어서 속도가 빠르기 때문에 실시간 데이터(실시간 영상 스트리밍)전송에 유리함
* 라우터에서는 VLAN을 인식할 수 없기 때문에 WAN 을 연결할 때 Untagged VLAN 사용
* 보안 취약점 존재 
> * Untagged VLAN은 Default값이 VLAN 1이기 때문에 이 설정값을 변경하지 않으면 Default값을 통해 외부의 침입자가 내부로 접근이 가능하게 됨

# VLAN 구성 방식
* End-to-End VLAN   
> * 물리적인 위치에 관계 없이 동일한 VLAN을 구성하는 방식   
> * VLAN이 전체 스위치에 걸쳐져 있기 때문에 사용자가 물리적인 위치를 이동해도 동일한 VLAN일 수 있음   
> * 장점 : 설정이 간편하고 편리(별 다른 VLAN구축이 필요 없고 하나만 만들어주면 됨)   
> * 단점 : 트래픽이 모두 Broadcast됨(트래픽이 많이 발생)   
![vlan4](https://user-images.githubusercontent.com/57285121/116401848-ac8d3d00-a866-11eb-867f-21f7c479a977.PNG)   

* Local VLAN
> * 물리적인 위치마다 각각 다른 VLAN을 구성하는 방식(End-to-End VLAN과 반대)   
> * 사용자가 물리적인 위치를 이동하게 되면 다른 VLAN에 소속 될 수 있음   
> * 장점 : 네트워크 구조를 확장하기 쉽고 트래픽 흐름 예측을 통해서 장애를 발견하기 쉽다. 이중화가 쉽다.   
> * 단점 : 설정과 관리가 복잡하고 상위계층의 장비(L3 스위치 or 라우터)가 필요함   
![vlan5](https://user-images.githubusercontent.com/57285121/116402525-7c926980-a867-11eb-90b9-a4ae51506a1c.PNG)   

* Static VLAN(Port기반)
> * 관리자가 직접 스위치의 포트에 VLAN을 할당
> * Default 설정 방식   
> * 관리자가 직접 관리와 설정을 해야함  
![svlan](https://user-images.githubusercontent.com/57285121/116406837-10fecb00-a86c-11eb-9bea-9ecc1a4cc4ef.PNG)   
 

* Dynamic VLAN(MAC주소/프로토콜 기반)
> * 스위치의 포트에 VLAN할당을 동적으로 자동화   
> * Static VLAN처럼 포트별로 VLAN을 할당하는 것이 아니고 포트에 접속하는 장비의 MAC주소에 따라 VLAN을 할당하는 방식   
> * VMPS(VLAN Membership Policy Server)에서 해당 장비의 MAC주소를 기반으로 할당할 VLAN을 준비해 놓고 요청이 들어왔을 때 할당할 VLAN정보를 스위치에 반환하고 해당 스위치가 VLAN 정보 세팅  
> * VMPS가 장애가 생기면 VLAN을 이용하는 모든 네트워크 서비스에 장애가 발생하게 됨   
> * 장비의 MAC주소에 따라 해당 네트워크를 자동으로 찾기 때문에 이동이 잦은 환경에서 사용하기 적합    
![dvlan](https://user-images.githubusercontent.com/57285121/116406930-28d64f00-a86c-11eb-86af-a6a4cae1159c.PNG)   

# VLAN 사용 목적
* 불필요한 브로드캐스트 트래픽 차단(과부하 감소)
* 네트워크를 분리하여 접근이 허가된 대상만 접근할 수 있도록 설정하여 보안성 향상 가능(보안성)
* 기존 네트워크의 물리적인 변화를 주지 않고도 구조를 변경할 수 있음(유연성)
* 이중화

