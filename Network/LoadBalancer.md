Load Balancer
=====================

# Load Balancer : 부하 분산, Load Balancing
* 서버의 사용자가 늘어나고, 그에 따라 규모가 커지게 되며 트래픽 증가
* Load Balancer는 클라이언트로부터 들어오는 다수의 요청을 서버들에게 적절히 배분하고 서버가 처리할 수 있도록 함(부하 분산, Load Balancing)
* Scale-Up / Scale-Out : 서버의 확장 목적   
> * Scale-Up : 서버의 성능 향상을 위해 서버 자체의 하드웨어를 업그레이드 하는 방법   
> * Scale-Out : 기존 운영중이던 서버의 수보다 많아지게 서버의 수를 증설하는 방법   
<img width="547" alt="스크린샷 2021-05-04 오후 9 41 06" src="https://user-images.githubusercontent.com/57285121/117004790-70a01f00-ad21-11eb-880f-d837a649541c.png">   

* Scale-Down / Scale-In : 서버의 축소 목적   
> * Scale-Down : 운영중이던 서버의 하드웨어 성능을 낮추는 방법   
> * Scale-In : 운영중이던 다수의 서버를 하나의 서버에 묶어 더 적은 수의 서버로 서비스를 제공하는 방법   
<img width="552" alt="스크린샷 2021-05-04 오후 9 41 55" src="https://user-images.githubusercontent.com/57285121/117004877-8e6d8400-ad21-11eb-8cf6-74ff86d1147a.png">   

# Load Balancer 주요 기능
* Health Check : 서버들의 장애 여부를 판단   
> * Health Check를 통해 서버들의 장애 여부를 판단해서 이상이 생길 시 Fail Over를 가능하게 해줌   
* NAT(Network Address Translation) : IP주소 변환. 외부와 통신을 하기위한 Virtual Server의 IP(VIP)와 내부 네트워크에서 사용하기 위한 사설 IP주소간 변환하는 역할(SNAT/DNAT)   
* Tunneling : 눈에 보이지 않는 통로를 만들어 통신. 클라이언트와 서버 사이에서 상호간 연결 되었을 때만 캡슐화된 패킷을 구별해 캡슐화 해제   
* DSR(Direct Server Return) Mode : 서버에서 클라이언트로 응답을 전달할 때 로드밸런서를 거치지 않고 바로 전달하는 방식. 로드밸런서의 부하를 줄여줄 수 있다.
> * 로드밸런서 자체의 부하룰 줄여주고 빠른 응답속도를 얻을 수 있지만 로드밸런서의 부하 분산 기능이 제대로 작동하지 않을 수도 있음   
* Proxy Mode : 클라이언트와 서버간 응답과 요청이 로드밸런서를 거치는 방법   
> * 부하 분산 기능을 할 수 있지만 로드밸런서 자체에 부하가 발생한다는 단점이 있음

# Load Balancing 알고리즘
* Round Robin   
> * 다수의 서버에게 순서대로 트래픽을 할당하는 방법. 차례대로 들어온 요청을 할당하여 분산   
<img width="529" alt="스크린샷 2021-05-04 오후 9 52 27" src="https://user-images.githubusercontent.com/57285121/117006130-07211000-ad23-11eb-9b75-111201c78689.png">   
* Least Connection   
> * 사용자와 서버가 정상적으로 연결을 맺으면 Connection 을 생성. 로드밸런서도 이 Connection 정보를 갖고 있고, Connection이 가장 적은 서버에게 요청을 할당하여 트래픽을 분산(가장 많이 사용)    
<img width="502" alt="스크린샷 2021-05-04 오후 9 54 13" src="https://user-images.githubusercontent.com/57285121/117006344-464f6100-ad23-11eb-97a5-1b3073b49994.png">   
* Weight or Ratio
> * 서버의 처리 능력을 확인하여 서버가 가질 수 있는 Connection 비율을 설정하고 해당 비율 만큼 요청을 할당하여 트래픽을 분산   
<img width="505" alt="스크린샷 2021-05-04 오후 10 05 23" src="https://user-images.githubusercontent.com/57285121/117007619-d510ad80-ad24-11eb-865e-34493d221209.png">   
* Response Time
> * 응답속도가 가장 빠른 서버에게 우선적으로 요청을 할당하여 트래픽을 분산.   
* Hash   
> * 특정 클라이언트는 특정 서버로만 할당. 경로가 보장되며 접속자 수가 많을 수록 효율이 뛰어남

# Load Balancer : 이중화, Fail Over
* 고가용성(HA, High Availability) : 서버의 고장 없이 지속적으로 정상적인 서버 운영이 가능한 상태
* 시스템에 장애가 발생할 경우에 대비하여 시스템의 기능을 계속 유지할 수 있도록 예비 장치를 운용
* 서비스가 중단되는 Downtime 최소화가 주 목적
* 여분의 서버, 네트워크 장비 등의 추가적인 자원이 필요
* Active/Standby   
> * 서버 한 대는 Active(활성상태), 다른 서버는 Standby(대기상태)로 동작   
> * 운영 중이던 Active상태의 서버가 시스템 장애 발생 시 Standby 상태의 서버를 Active상태로 바꾸고 서비스를 시작   
<img width="537" alt="스크린샷 2021-05-05 오전 12 19 24" src="https://user-images.githubusercontent.com/57285121/117027339-90424200-ad37-11eb-9a87-9757050bba65.png">   
Passive = Standby
