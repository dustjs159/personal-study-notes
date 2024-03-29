💻 [AWS] EC2 Placement Group
==============================

* Placement Group : EC2 인스턴스의 배치 방식을 정의
* 그룹에 대한 비용은 무료(그룹 내 인스턴스 비용은 당연히 청구됨)

## 배치 그룹 유형
* Cluster
* Spread
* Partition

### Cluster
<img width="247" alt="스크린샷 2023-06-06 오후 12 58 04" src="https://github.com/dustjs159/Study/assets/57285121/a05d182f-f815-4713-9591-410cb57e4360">

* 짧은 Latency를 위해 그룹 내 인스턴스를 단일 AZ, 동일 Lack에 배치
    * Latency가 적다는 장점이 있으나 하드웨어 장애 발생 시 모든 인스턴스의 장애가 발생할 수 있다는 단점이 있음
    * 보다 더 적은 지연시간을 필요로 하는 app 배포에 유용

### Spread
<img width="489" alt="스크린샷 2023-06-06 오후 1 04 13" src="https://github.com/dustjs159/Study/assets/57285121/c8379349-2012-4269-9111-d84e63d460e4">

* 그룹 내 모든 인스턴스를 고유한 하드웨어에 배치
    * 각각 고유한 하드웨어에서 인스턴스가 실행됨(1 하드웨어 : 1 인스턴스)
    * 동일한 하드웨어를 공유하고 있는 인스턴스보다 상대적으로 장애 확률이 적다는 장점이 있으나 AZ 내 그룹당 인스턴스 7개 제한
    * 지연시간보다 가용성을 더 필요로 하는 app 배포에 유용

### Partition
<img width="389" alt="스크린샷 2023-06-06 오후 1 02 00" src="https://github.com/dustjs159/Study/assets/57285121/29e050f6-7c39-4c84-a7b7-815311f90874">

* 단일 AZ 내 파티션이라는 이름의 논리적인 그룹에 인스턴스를 포함
    * 각각의 파티션은 고유한 하드웨어에 배치됨
    * AZ당 파티션 개수는 7개로 제한됨(파티션 내 인스턴스 수 제한은 없음)
    * 파티션 내 인스턴스들이 고유한 데이터를 보유하고 있어야 할 app 배포에 유용
