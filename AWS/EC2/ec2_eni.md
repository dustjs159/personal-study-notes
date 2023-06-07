💻 [AWS] EC2 Elastic Network Interface
======================================

* Elastic Network Interface (ENI) : 인스턴스의 가상 네트워크 카드
    * 인스턴스의 Security Group이 적용되는 지점.
    * 인스턴스를 생성할 때 선택한 VPC IPv4 CIDR 내에서 IP를 할당 받는 대상
        * 이게 없으면 IP를 할당 받지 못하니 당연히 네트워크 통신이 되지 않음!
        * 인스턴스 생성 시 private IPv4가 할당되는 primary network interface의 이름은 `eth0`
    * 인스턴스에 Attach / Detach 가능 (Elastic이 붙은 이유)
    * 하나의 인스턴스에 여러 ENI를 Attach할 수 있지만 하나의 ENI를 여러 인스턴스에 Attach할 수 없음
    * AZ Level
    * ENI 자체에 대한 비용은 무료    

## ENI Type
* VPC Endpoint
* Network Load Balancer (NLB)

## ENI 교체하기
* 인스턴스가 생성될 때 함께 생성되는 primary ENI (eth0)는 교체가 될까? 라는 의문이 들어 테스트 해봤는데, primary ENI는 **교체 불가**
    * 교체하려면 인스턴스 교체를 해야함.

## 여러 EIP가 할당된 ENI가 여러개 attach될 경우
* Elastic IP가 할당된 ENI가 인스턴스에 다수 attach한 상태에서 Public IP를 조회해보니 primary ENI (eth0) 의 Public IP만 조회된다.
