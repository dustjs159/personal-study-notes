💻 [AWS] AWS EC2
================
* Amazon EC2 (Elastic Compute Cloud)
  * AWS의 데이터 센터 내 물리적인 장비 위에서 작동하는 Virtual Machine(By Hypervisor)
    * Hypervisor : 물리적인 하드웨어 장비(Host)와 VM 사이에서 작동하는 소프트웨어로써 물리적인 리소스 자원을 가상화하여 VM에 할당하는 역할을 한다.
  * EC2 서비스를 통해 생성되는 VM은 **인스턴스**라는 이름으로 생성됨
  * AWS에서 지원하는 인스턴스 유형의 종류가 다양하기 때문에 인스턴스에서 실행할 app의 특성과 비용을 고려하여 인스턴스를 선택할 수 있도록 한다.
  * AZ Level 서비스

## Instance
* 인스턴스(Instance) : VM의 생성 단위
* 인스턴스 구성 요소
  * OS : 인스턴스의 운영체제
    * Amazon Linux, Ubuntu, RedHat, Windows 등 여러 OS를 선택하여 사용 가능
  * vCPU & Memory : 인스턴스의 스펙
  * Storage : 인스턴스의 데이터 저장소
    * EBS Volume, EFS 등 여러 스토리지 유형 사용 가능
  * Network : 인스턴스를 배치할 VPC / Subnet 선택
  * Security Group : 인스턴스의 방화벽
* 별도의 구매 옵션이 없는 경우 인스턴스를 생성한 시점부터 비용이 청구됨.(인스턴스 생성 후 1초만 사용해도 1시간 요금이 적용된다.)