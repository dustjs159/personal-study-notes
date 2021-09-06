Amazon ELB
====================================
## Summary
- Last Updated : 21.09.03 Fri   
- Updated by : YEONSUN YOON
-----------------------------------

# 네트워크 부하 분산(로드밸런싱)

* 부하 분산이란 처리해야 할 요청을 나누어 처리 하는 것을 말합니다.
* 네트워크 측면에서 이를 **로드밸런싱(Load Balancing)** 이라고 합니다.
* 서버를 운영하게 되면 규모가 커짐에 따라 자연스럽게 클라이언트의 요청이 늘어날 수 밖에 없고 서버에 과부하가 오게 되어 서버에 장애가 생길 수 있습니다. 이 때 서버를 **Scale-Out** 하고 **로드밸런싱**을 통해 적절하게 요청을 분배하여 처리할 필요가 있습니다.
* 로드밸런싱을 통해 **고가용성**을 유지할 수 있습니다.
   
<img width="424" alt="스크린샷 2021-09-02 오후 5 44 41" src="https://user-images.githubusercontent.com/57285121/131812622-57ada7d6-77cc-4f60-9d33-0fa8adc5a5fb.png">
   
<img width="424" alt="스크린샷 2021-09-02 오후 5 46 13" src="https://user-images.githubusercontent.com/57285121/131812903-af0ee2d4-b387-45b0-bde3-06f6e3a9fccf.png">
   
> * 서버 하나만으로 서비스를 운영하다 보면 서버에 장애가 왔을 때 필연적으로 서버를 중단해야 합니다.**(고가용성 하락)** 하지만 여러 대의 서버를 배치하고 로드밸런싱을 통해 적절하게 요청을 분배하면 서버의 장애를 예방할 수 있을 뿐더러 서버의 장애가 생겨도 서버 중단 없이 다른 서버에서 요청을 처리할 수 있다는 장점이 있습니다.   

# AWS ELB
* AWS ELB(Elastic Load Balancing)는 AWS에서 제공하는 **로드 밸런싱**기능입니다.
* EC2 인스턴스에 수신되는 트래픽을 여러 인스턴스로 분배하여 **고가용성 환경**을 구성할 수 있도록 해줍니다.
   
<img width="510" alt="스크린샷 2021-09-02 오후 5 57 01" src="https://user-images.githubusercontent.com/57285121/131814673-bdb19d05-e72f-4822-887d-7498f22fdef0.png">
   
# AWS ELB 구성
   
<img width="501" alt="스크린샷 2021-09-02 오후 6 41 39" src="https://user-images.githubusercontent.com/57285121/131821521-36219d7d-1216-41de-a762-8b4ae0b72661.png">
   
리스너(Listenr)   
* 프로토콜 및 포트를 사용하여 연결 요청을 확인합니다. 로드밸런서에서 부하 분산을 하기 위한 프로토콜과 포트를 지정하는 규칙(Rule)을 생성합니다.
   
대상 그룹(Target Group)   
* 부하 분산을 위해 하나 이상의 대상을 대상 그룹으로 지정합니다. 그룹 내 대상들에 대해 주기적으로 확인하고 정상적인 상태의 대상에게만 트래픽을 전달합니다.

# AWS ELB 종류
   
<img width="1095" alt="스크린샷 2021-09-02 오후 6 28 17" src="https://user-images.githubusercontent.com/57285121/131819567-d9e249e2-7bcb-427d-a71e-4e1807ae1ce8.png">
   
* ALB(Application Load Balacner)
* NLB(Network Load Balancer)
* GLB(Gateway Load Balancer)
* CLB(Classic Load Balancer)

## ALB(Application Load Balacner)

