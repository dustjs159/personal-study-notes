💻 [AWS] RDS Multi AZ
=============================
# RDS Mutli AZ
* 가용성을 위해 클러스터 내 RDS 인스턴스들을 여러 AZ에 걸쳐 배치
    * 주로 재해복구(Disaster Recovery) 목적
* Active-Standby 구조로 동작
    * 지속적으로 Active <-> Standby가 Data Sync
    * 하나의 Endpoint로 Active DB에 접근하고 Active DB가 장애가 발생할 경우 자동으로 Standby가 Active로 승격
* 읽기 전용 복제본도 다중 AZ 설정이 가능
* 단일 AZ -> 다중 AZ 적용 시 다운타임 없음!