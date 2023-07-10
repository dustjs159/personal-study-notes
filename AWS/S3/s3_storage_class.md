💻 [AWS] S3 Storage Class
==================

# S3 스토리지 클래스
* S3 버킷의 요구사항(액세스 빈도, 아카이빙 등)에 따라 선택할 수 있는 최적화된 스토리지 유형을 제공
* 보다 저렴하게 S3 버킷을 사용하기 위해 상황에 맞게 적절한 클래스를 선택하는 것이 중요!

## S3 Standard
* 가장 보편적인 스토리지 클래스
* 스토리지 클래스중 데이터 액세스가 가장 빈번하게 일어나는 경우에 적절
* 별도로 스토리지 클래스를 지정하지 않은 경우 Default 값으로 S3 Standard를 사용하게 된다.

## S3 Intelligent-Tiering
* 데이터가 저장되는 버킷을 3-Tier로 나누어 저장.
  * Tier1 : Frequent Access
  * Tier2 : Infrequent Access
    * 접근한지 30일이 지나면 여기 티어에 저장됨. Standard에 비해 약 40% 저렴하기 때문에 장기적인 백업 용도로 사용하면 좋을 듯 하다.
  * Tier3 : Archive Instant Access
    * 접근한지 90일이 지나면 여기 티어에 저장됨. Standard에 비해 약 68% 저렴하기 때문에 거의 액세스하지 않는 데이터 백업 용도로 적절.
* Tier가 변경된 후, 다시 액세스하게 되면 Frequent Access Tier로 변경되어 Standard 요금이 적용된다. 따라서 버킷 내 오브젝트 액세스가 불규칙적일 경우 사용.

## S3 Standard IA
* 자주 액세스 할 필요는 없지만 필요할 때 빠른 시간 내에 액세스 해야할 경우 적합
* Standard보다는 저렴하다.
* S3 Intelligent-Tiering에서 Tier2(Infrequent Access)에 해당하는 클래스

## S3 One-Zone IA
* 일반적으로 S3의 스토리지들은 최소 3개 이상의 가용 영역에 저장되지만 S3 One Zone-IA는 하나의 가용 영역에만 데이터를 저장
* 하나의 가용 영역에만 저장하기 때문에 S3 Standard-IA에 비해 상대적으로 비용이 저렴
* 비용은 상대적으로 저렴하나, 하나의 가용 영역에만 데이터가 저장되기 때문에 가용성이 떨어지게 된다는 단점. 따라서 가용성이 낮아도 큰 문제가 없는 데이터들을 S3 One Zone-IA에 저장하여 비용을 낮출 수 있음

## S3 Glacier Instant Retrieval
* 거의 액세스가 필요하지 않은 아카이빙용 버킷이긴 하나 분기당 한번 정도의 액세스가 필요한 경우 선택
* 아카이빙용 버킷 중 가장 액세스 속도가 빠름.
* S3 Standard IA보다 약 68% 저렴한 비용
* S3 Intelligent-Tiering에서 Tier3(Archive Instant Access)에 해당하는 클래스

## S3 Glacier Flexible Retrieval
* 마찬가지로 아카이빙용 버킷. 연 1~2회 정도의 액세스가 필요한 경우 선택
* S3 Glacier Instant Retrieval보다 10%정도 저렴
* 즉각적인 액세스는 어려우나(몇 분 ~ 몇 시간 소요) 대규모 데이터에 무료로 액세스할 수 있음.

## S3 Glacier Deep Archive
* 아카이빙용 버킷중 가장 저렴. 연 1회 정도의 액세스가 필요하고 **컴플라이언스** 준수 목적(7~10년동안 자료 보관 등)을 위해 선택
* 액세스에 최대 12시간 소요됨