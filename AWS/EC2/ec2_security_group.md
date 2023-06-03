💻 [AWS] EC2 Security Group
===========================

# 인스턴스의 방화벽 - 보안 그룹(Security Group)
* 인스턴스에 대한 트래픽을 제어하는 **방화벽**
* **보안 그룹이 적용되는 지점은 인스턴스의 ENI(Elastic Network Interface)**
* Inbound / Outbound 트래픽에 대해 허용할 규칙 지정
  * Inbound 규칙 : 프토토콜, 포트번호, Source IP 지정
  * Outbound 규칙 : 프로토콜, 포트번호, Destination IP 지정
  * 이 때 각 **IB/OB 규칙에 특정 보안 그룹을 지정하여 사용할 수 있다.**
    * 이렇게 되면 IP 주소가 바뀌어 서비스 장애가 발생할 상황에 대비할 수 있기에 VPC 내부의 리소스에 접근하고자 할 떄는 보안 그룹의 각 규칙에 IP 주소보다는 출발지 or 목적지의 보안그룹을 설정하는 것이 좋다.

