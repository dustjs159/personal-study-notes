💻 [AWS] AWS ELB
===============
# 💡 AWS ELB
* AWS ELB(Elastic Load Balancing)는 AWS에서 제공하는 **로드 밸런싱**기능
* EC2 인스턴스에 수신되는 트래픽을 여러 인스턴스로 분배하여 **고가용성 환경**을 구성할 수 있도록 함(접점 역할)
* 최소 2개의 가용 영역을 사용하여 고가용성을 보장하도록 구성

# 네트워크 부하 분산(로드밸런싱)

* 부하 분산이란 처리해야 할 요청을 나누어 처리 하는 것
* 네트워크 측면에서 이를 **로드밸런싱(Load Balancing)** 이라고 함
* 서버를 운영하게 되면 규모가 커짐에 따라 자연스럽게 클라이언트의 요청이 늘어날 수 밖에 없고 서버에 과부하가 오게 되어 서버에 장애가 생길 수 있는데, 이 때 서버를 **Scale-Out** 하고 **로드밸런싱**을 통해 적절하게 요청을 분배하여 처리
* 로드밸런서는 서버들의 상태를 파악하고 요청을 분산하여 전달하는 역할을 수행(고가용성을 유지) 
   
<img width="424" alt="스크린샷 2021-09-02 오후 5 44 41" src="https://user-images.githubusercontent.com/57285121/131812622-57ada7d6-77cc-4f60-9d33-0fa8adc5a5fb.png">
   
<img width="424" alt="스크린샷 2021-09-02 오후 5 46 13" src="https://user-images.githubusercontent.com/57285121/131812903-af0ee2d4-b387-45b0-bde3-06f6e3a9fccf.png">
   
> * 서버 하나만으로 서비스를 운영하다 보면 서버에 장애가 왔을 때 필연적으로 서버를 중단해야 합니다.**(고가용성 하락)** 하지만 여러 대의 서버를 배치하고 로드밸런싱을 통해 적절하게 요청을 분배하면 서버의 장애를 예방할 수 있을 뿐더러 서버의 장애가 생겨도 서버 중단 없이 다른 서버에서 요청을 처리할 수 있다는 장점이 있습니다.   


# AWS ELB

   
<img width="510" alt="스크린샷 2021-09-02 오후 5 57 01" src="https://user-images.githubusercontent.com/57285121/131814673-bdb19d05-e72f-4822-887d-7498f22fdef0.png">
   
# AWS ELB 구성
   
<img width="501" alt="스크린샷 2021-09-02 오후 6 41 39" src="https://user-images.githubusercontent.com/57285121/131821521-36219d7d-1216-41de-a762-8b4ae0b72661.png">
   
리스너(Listenr)   
* 프로토콜 및 포트를 사용하여 연결 요청을 확인합니다. 로드밸런서에서 부하 분산을 하기 위한 프로토콜과 포트를 지정하는 규칙(Rule)을 생성합니다.
   
대상 그룹(Target Group)   
* 부하 분산을 위해 하나 이상의 대상을 대상 그룹으로 지정합니다. 그룹 내 대상들에 대해 주기적으로 확인하고 정상적인 상태의 대상에게만 트래픽을 전달합니다.

# AWS ELB 통신 방식

인터넷 연결(Internet Facing Load Balancing)
   
<img width="503" alt="스크린샷 2021-10-05 오후 1 27 28" src="https://user-images.githubusercontent.com/57285121/135960063-e0693da5-1279-43ff-accc-69115d4cfa87.png">
   
- 퍼블릭 IP 주소를 갖고 있기 때문에 외부에서 로드밸런서에 직접 접근이 가능
- 로드밸런서는 연결된 인스턴스로 요청을 라우팅

내부 연결(Internal Load Balancing)
   
<img width="486" alt="스크린샷 2021-10-05 오후 1 29 05" src="https://user-images.githubusercontent.com/57285121/135960237-a766f41e-60f8-422f-bb68-ebfa2f1eb1f3.png">
   
- 프라이빗 IP 주소만 갖고 있기 때문에 외부에서의 접근을 차단하고 VPC 내부에서만 접근이 가능

교차 영역 로드밸런싱(Cross-Zone Load Balancing)

- 기본적으로 ELB는 Round-Robin 알고리즘으로 요청을 분산(여러 트래픽의 우선순위를 정하지 않고 시간 순서에 따라 하나씩 분산)
- 가용 영역 내 인스턴스의 수가 다르게 존재하는 경우 가용 영역 내 인스턴스에 대한 부하 불균형이 발생할 수 있는데, 이를 해결하기 위한 방법이 교차 영역 로드밸런싱
- 기본적으로 NLB는 비활성화, ALB는 활성화
- 비활성화 상태
   
<img width="1000" alt="스크린샷 2021-10-05 오후 2 43 17" src="https://user-images.githubusercontent.com/57285121/135966940-fbd21067-b4d9-4418-97b4-b85b38dcf680.png">
    
![Untitled 8](https://user-images.githubusercontent.com/57285121/135965781-41dd82f7-dd1c-4bed-8d4a-dd076a904b1f.png)
   
> - 각각 인스턴스에 부하 불균형 발생

- 활성화 상태
   
<img width="1000" alt="스크린샷 2021-10-05 오후 2 44 01" src="https://user-images.githubusercontent.com/57285121/135967008-38a5b1b6-ac97-4bcb-acda-a9b858016690.png">
    
![Untitled 10](https://user-images.githubusercontent.com/57285121/135965874-2112d466-5425-40b6-8899-7176634f0628.png)
   
> - 각각 인스턴스에 골고루 부하 전달

# AWS ELB 종류
   
<img width="1095" alt="스크린샷 2021-09-02 오후 6 28 17" src="https://user-images.githubusercontent.com/57285121/131819567-d9e249e2-7bcb-427d-a71e-4e1807ae1ce8.png">
   
ALB(Application Load Balancer)   
- HTTP/HTTPS에 가장 적합한 로드 밸런서.
- OSI 모델중 7계층(애플리케이션 계층)에 해당
- 웹 애플리케이션에 대한 트래픽을 URI단위로 분산할 수 있기 때문에 세밀한 분산이 가능하다는 장점
- 처리 속도가 상대적으로 느리며 고정 IP 설정이 불가능(IP가 유동적)
   
NLB(Network Load Balancer)
- TCP/UDP/TLS에 가장 적합한 로드 밸런서.
- OSI 모델중 4계층(전송 계층)에 해당
- 트래픽의 패킷만을 확인하여 분산하기 때문에 ALB에 비해 세밀한 분산이 어렵다는 단점
- 처리 속도가 상대적으로 빠르며 **고정 IP 설정이 가능**
   
GLB(Gateway Load Balancer)    
- OSI 모델중 3계층(네트워크 계층)에 해당

CLB(Classic Load Balancer)   
- 이전 세대의 로드밸런서
- 지원하는 프로토콜이 많다는 장점이 있으나 주로 ALB, NLB로 대체됨

# Lab

