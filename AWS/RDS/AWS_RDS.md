💻 [AWS] AWS RDS 
==================
# 💡 AWS RDS
* AWS RDS(Relational Database Service)
    * **관계형 DB**를 AWS 서비스로 제공
        * 관계형 DB내 데이터들은 정형화 데이터들이 존재
        * 비관계형 DB(NoSQL)를 제공하는 서비스로는 DynamoDB, ElastiCache, DocumentDB 등이 있다.
    * Managed Service : 패치, 백업 등의 관리적인 측면을 AWS가 담당해주기 때문에 관리 포인트가 줄어들 수 있음

## 📌 RDS 기본 
* 기본적으로 RDS는 내부적으로 EC2 + EBS 볼륨 조합으로 구성. EC2와 마찬가지로 VPC, 서브넷 등의 네트워킹을 기반으로 한 VM 위에서 동작
    * VPC, 서브넷, SG 등을 지정해줘야하며 마찬가지로 인스턴스 및 EBS 볼륨 유형도 선택 가능
    * 단, 직접 시스템에 접근이 불가능. EC2는 Putty나 Mac 터미널 등을 통해 시스템에 접근할 수 있지만 RDS는 접근이 불가능함 → **OS 패치 등의 시스템 관리는 AWS가 담당**
* RDS Endpoint를 통해 DNS로 접근한다.
* Public IP가 자동으로 할당되지 않음

## 📌 RDS 인증 방식
* User/Password
* IAM 
* Kerberos

## 📌 RDS 지원 엔진
* 라이센스 별도 비용 지불이 필요한 엔진
    * MS SQL Server, Oracle 
* 오픈소스 기반으로 별도 라이센스 비용 지불이 필요하지 않은 엔진
    * MySQL Server
    * Postgre SQL
    * MariaDB
    * **Amazon Aurora**
    

## 📌 Amazon Aurora MySQL 버전 업그레이드

* Aurora MySQL 버전 1 (MySQL 5.6)의 2023-02-28 EOL(End Of Life)에 따른 버전 업그레이드 진행 필요
    * Aurora MySQL 버전 2 ==> MySQL 5.7
    * Aurora MySQL 버전 3 ==> MySQL 8.0
* Aurora MySQL 버전 1 → 버전 3 불가능
    * 순차적으로 가야함. 버전 1 → 2 → 3
    * 1.x → 2.x 참조 문서
        * https://docs.aws.amazon.com/ko_kr/AmazonRDS/latest/AuroraUserGuide/AuroraMySQL.Updates.MajorVersionUpgrade.html#AuroraMySQL.Updates.MajorVersionUpgrade.1to2
    * 2.x → 3.x 참조 문서
        * https://docs.aws.amazon.com/ko_kr/AmazonRDS/latest/AuroraUserGuide/AuroraMySQL.Updates.MajorVersionUpgrade.html#AuroraMySQL.Updates.MajorVersionUpgrade.2to3
* 현재 위치에서 DB 클러스터의 버전을 업그레이드(In-Place)하는 방법과 스냅샷 복구를 통해 버전 업그레이드를 하는 방법 두 가지가 존재.

### 1.x → 2.x 업그레이드
* 엔진 속성 변경
    * `aurora` → `aurora-mysql`
    
