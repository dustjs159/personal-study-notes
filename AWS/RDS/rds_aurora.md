💻 [AWS] Amazon Aurora
=============================
# Amazon Aurora
* 확장가능한 RDS 
* PostgreSQL, MySQL과 호환됨
* DB Storage 자동 확장 10GB ~ 128TB
* RO 복제본 최대 15개까지 가능
    * RDS MySQL은 최대 5개.
* DB 데이터가 3개의 AZ에 걸쳐 AZ당 2개씩 총 6개의 복제 볼륨 내에 저장됨
* RDS와 마찬가지로 하나의 RW-DB(master)가 존재하며 여러 AZ에 걸쳐 RO-DB 복제본(Standby)이 있고 RW-DB가 장애 발생시 30초 이내에 RO-DB가 RW-DB로 승격
    * DB 생성 시 RW-DB / RO-DB Endpoint 두 개가 생성된다.

# 부가기능? 주요기능?
* Custom Endpoint
* Multi-Master
* Aurora Serverless
* Global Aurora - 리전간 복제
* 머신러닝 서비스와 통합 가능
    * SageMaker, Comprehend 등등..
