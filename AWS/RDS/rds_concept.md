💻 [AWS] Amazon RDS 
====================
# Amazon RDS
* Amazon RDS(Relational Database Service) : **관계형 데이터 베이스**
    * 정형 데이터 저장을 위한 관리형 DB

# RDS 기본 
* 기본적으로 RDS는 내부적으로 EC2 + EBS 볼륨 조합으로 구성. EC2와 마찬가지로 VPC, 서브넷 등의 네트워킹을 기반으로 한 VM 위에서 동작
    * VPC, 서브넷, SG 등을 지정해줘야하며 마찬가지로 인스턴스 및 EBS 볼륨 유형도 선택 가능
    * 단, 직접 시스템에 접근이 불가능. EC2는 Putty나 Mac 터미널 등을 통해 시스템에 접근할 수 있지만 RDS는 접근이 불가능함 → **OS 패치 등의 시스템 관리는 AWS가 담당**
* RDS를 선택하는 이유
    * EC2 인스턴스에 MySQL을 설치해서 사용해도 되는데 RDS를 사용하는 이유는, 별도 서버를 관리하지 않아도 되는 **관리형 서비스**이기 때문에 관리포인트가 줄어든다는 장점 때문. 

# RDS 지원 엔진
* 라이센스 별도 비용 지불이 필요한 엔진
    * MS SQL Server, Oracle 
* 오픈소스 기반으로 별도 라이센스 비용 지불이 필요하지 않은 엔진
    * **MySQL Server**
    * **Postgre SQL**
    * **MySQL MariaDB**
    * **Amazon Aurora**

