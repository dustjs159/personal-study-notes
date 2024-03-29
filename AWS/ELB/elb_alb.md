💻 [AWS] ALB
=================
## ALB (Application Load Balancer)
* HTTP/HTTPS 요청에 대한 트래픽 분산 처리 - L7 스위치 역할
    * HTTP/HTTPS 트래픽을 라우팅하는 용도로 사용.
* **IP 고정이 불가능.** 대신 DNS Record를 제공하여 도메인으로 접근할 수 있도록 함.

## Listener
* Listener : 외부로부터 request를 받아 라우팅하는 역할
* ALB가 전달받은 HTTP/HTTPS request를 받아 Target Group에 전달할 때 추가되는 헤더
    * X-Forwarded-For
    * X-Forwarded-Proto
    * X-Forwarded-Port

## Target Group
* Target Group : 전달할 대상
    * 그룹에 포함시킬 수 있는 대상은 EC2 인스턴스, Lambda 함수, Private IP 등이 있음

## 교차 영역 로드 밸런싱
* 단순히 AZ 단위로만 트래픽을 분산하는 것이 아닌 AZ내 Target의 수 까지 고려하여 트래픽을 분산
    * ALB은 default로 활성화 되어있는 기능
```vim    
교차 영역 로드밸런싱이란 ALB가 배치되어 있는 두 AZ에 트래픽을 로드 밴런싱 할 때 50/50씩 트래픽을 분산하지 않고 Target의 수를 고려하여 분산을 한다. 예를 들어 AZ-1에 인스턴스 2대, AZ-2에 인스턴스 8대가 있다고 가정을 한다면 두 AZ에 트래픽 분산을 50/50으로 하는 것이 아닌 20/80으로 트래픽을 분산한다.

50/50씩 분산하게 되면 AZ-1의 인스턴스는 각 25의 트래픽을 처리할 것이고 AZ-2의 인스턴스는 6.25씩 트래픽을 처리하게 될 것이다. 이렇게 되면 AZ-1의 인스턴스의 가용성이 떨어질 수 있기에, 20/80으로 트래픽을 분산하여 두 AZ 내 인스턴스가 모두 10의 트래픽만을 처리하도록 한다.
```

## ALB에 IP를 고정할 수 없는 이유
* ALB는 NLB와 다르게 고정 IP을 할당할 수 없다. 왜 그럴까?
```vim
우선, 고정 IP가 할당되는 주체는 네트워크 인터페이스다(ENI, Elastic Network Interface). 네트워크 인터페이스의 IP 주소는 VPC 내에서 DHCP로 할당을 받는다. 웹 콘솥에서 ALB의 ENI와 NLB의 ENI를 확인해보면 Interface Type이 다른 것을 확인할 수 있다.
```
*  ALB: `Elastic network interface`
*  NLB : `network_load_balancer`

```vim
AWS에서 제공하는 ALB는 HTTP/HTTPS 요청을 처리하기 위한 장비다. 그래서 IP 기반으로 요청을 처리하기 보단 DNS 기반으로 요청을 처리하는 것이 주 목적이기에 ALB 장비에 고정 IP 할당의 기능을 제외한 네트워크 인터페이스를 사용하는 것. 따라서 ALB의 ENI에는 고정 IP를 할당하는 것이 불가능하다.
```

* 그런데 EC2 인스턴스의 ENI와 ALB의 ENI의 Interface Type은 Elastic network interface로 동일한 것을 할 수 있다.
```vim
이것은 단순히 역할의 차이다. 둘의 장비가 유사하긴 하나 ALB에는 주 목적인 트래픽 분산을 위한 ENI가 탑재되어 있는 것이고 EC2 인스턴스에는 보다 범용성있는 ENI가 탑재되어 있다고 볼 수 있다.
```
## ALB는 IP가 바뀔 수도 있을까?

## ALB에서의 Health Check

## ALB에 여러 인증서를 적용
* HTTPS 리스너에 인증서 여러개를 적용할 수 있음.
