💻 [AWS] EC2 Elastic Network Interface
======================================

* Elastic Network Interface (ENI) : 인스턴스의 가상 네트워크 인터페이스
    * 인스턴스의 Security Group이 적용되는 지점.
    * 인스턴스를 생성할 때 선택한 VPC IPv4 CIDR 내에서 IP를 할당 받는 대상
        * 이게 없으면 IP를 할당 받지 못하니 당연히 네트워크 통신이 되지 않음!
    * 인스턴스에 Attach / Detach 가능 (Elastic이 붙은 이유)
    * 하나의 인스턴스에 여러 ENI를 Attach할 수 있지만 하나의 ENI를 여러 인스턴스에 Attach할 수 없음

# ENI Type
* VPC Endpoint
* Network Load Balancer (NLB)