💻 [AWS] AWS EC2
=============
* Amazon EC2
  * AWS의 데이터 센터 내 물리적인 장비 위에서 작동하는 Virtual Machine
  * EC2 서비스를 통해 생성되는 VM은 **인스턴스**라는 이름으로 생성됨
  * 여러 인스턴스 유형이 존재하고, 인스턴스에서 실행할 Application의 특성에 맞는 인스턴스 유형을 선택하여 생성 가능
  * AZ Level 서비스

# Instance
* 인스턴스(Instance) : VM 생성 단위
* 인스턴스 구성 요소
  * OS : 인스턴스의 운영체제
    * Amazon Linux, Ubuntu, RedHat, Windows 등 여러 OS를 선택하여 사용 가능
  * vCPU & Memory : 인스턴스의 스펙
  * Storage : 인스턴스의 데이터 저장소
    * EBS Volume, EFS 등 여러 스토리지 유형 사용 가능
  * Network : 인스턴스를 배치할 VPC / Subnet 선택
  * Security Group : 인스턴스의 방화벽