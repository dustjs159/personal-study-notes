💻 [AWS] AWS ELB
=================
* AWS ELB(Elastic Load Balancer) : 클라이언트로 부터의 요청을 하나 이상의 대상에게 전달하는 트래픽 분산기
* 트래픽 수신 대상은 EC2 인스턴스, Lambda 함수, 컨테이너 등이 될 수 있고 특정 IP를 지정할 수도 있음
* 가용성을 위해 둘 이상의 AZ 지정이 필요
* Security Group을 통해 접근 제어

## ELB 유형
(Classic Load Balancer는 제외)
* ALB(Application Load Balancer)
* NLB(Network Load Balancer)
* GLB(Gateway Load Balancer)

## 로드 밸런싱 알고리즘
* Round Robin
    * Round Robin 알고리즘은 각 인스턴스에 차례로 요청을 전달하는 방식입니다. 이 알고리즘은 각 인스턴스가 동일한 처리 능력을 가정하고 요청을 공평하게 분산하는 데 효과적입니다.
* Least Connection
    * Least Connection 알고리즘은 연결이 가장 적은 인스턴스에 요청을 보내는 방식입니다. 이 알고리즘은 인스턴스의 처리 능력이 서로 다를 때 효과적입니다.
* IP Hash
    * IP Hash 알고리즘은 클라이언트의 IP 주소를 기반으로 요청을 분산하는 방식입니다. 이 알고리즘은 동일한 IP 주소를 가진 클라이언트가 항상 동일한 인스턴스로 요청을 보내도록 보장합니다.
* Least Time
    * Least Time 알고리즘은 응답 시간이 가장 짧은 인스턴스에 요청을 보내는 방식입니다. 이 알고리즘은 인스턴스의 처리 능력과 응답 속도가 서로 다를 때 효과적입니다.

## ELB Type
* Internet-facing : Public ELB
* Internal : Private ELB
