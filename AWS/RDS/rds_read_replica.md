💻 [AWS] RDS Read Replica 
=============================
# RDS Read Replica
* 읽기 전용 복제본
    * 단순 조회 쿼리(SELECT)만 실행하는 app이 단일 DB대상으로 쿼리를 실행하는 경우 DB에 부하가 발생하여 서비스 장애가 발생할 수 있음.
    * 이를 대비해 RO-DB를 생성하고 Read 작업만 수행하는 app의 트래픽을 RO-DB로 전환.
* 작동 원리
    * RW-DB와 RO-DB가 비동기식으로 Data Sync를 맞춤.

## Pricing
* EC2 인스턴스는 서로 다른 AZ간의 통신에는 비용이 청구되지만 서로 다른 AZ의 RDS 인스턴스(RW-DB <-> RO-DB)간 통신 비용은 청구되지 않으나, 서로 다른 리전일 경우에는 청구됨.