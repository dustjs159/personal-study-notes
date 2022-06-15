💻 [AWS] Amazon S3
==================
# 💡 Amazon S3 

* Amazon S3(Simple Storage Service) : 객체(Object) 스토리지 서비스
* **Bucket** 단위로 데이터를 저장하며 Bucket에 데이터를 저장한 만큼 비용이 청구됨
* **정적 웹 페이지 호스팅 가능**
* Regional Service
* IAM 정책을 통해 Bucket에 대한 CRUD 권한 제어 가능
* AWS KMS 서비스를 통해 Bucket에 데이터를 전송 혹은 저장 시 데이터 암호화 가능 
* Bucket에 데이터 업로드 혹은 다운로드 등의 이벤트 발생시(Trigger) 알림 전송 가능
  * AWS SQS, SNS, Lambda
* **CloudFront** 서비스와 통합 가능
  * CloudFront의 엣지 로케이션과 S3 버킷 간 파일 업로드 및 다운로드하는 방식을 통해 매우 빠른 속도를 보장
  * **CloudFront + S3 조합으로 정적 웹 페이지를 호스팅**


## 📌 S3 스토리지 클래스

* S3 Standard
  * 가장 보편적인 스토리지 클래스
  * 스토리지 클래스중 데이터 액세스가 가장 빈번하게 일어나는 경우에 적절
  * 버킷에 객체를 업로드할 때 스토리지 클래스를 지정하지 않은 경우 Default 값으로 S3 Standard를 사용
* S3 Intelligent-Tiering
  * 데이터가 저장되는 곳을 두 계층으로 나누어 Frequent 계층에는 데이터 액세스가 잦은 데이터가 저장되고 Infrequent 계층에는 상대적으로 데이터 액세스가 적은 데이터들을 **분리하여 저장**
  * 데이터 액세스를 패턴을 모니터링하여 두 계층 간 데이터를 자동으로 이동
  * 데이터 액세스가 불규칙적인 경우에 데이터를 분리 저장하여 비용을 줄이고자 할 때 사용
* S3 Standard-IA(Infrequent Access)
  * S3 Standard와 동일한 성능
  * S3 Standard보다 데이터 액세스가 적게 발생할 경우에 S3 Standard-IA 를 선택하여 비용을 낮출 수 있음
  * 자주 액세스하지 않지만 필요할 때 빠르게 데이터에 액세스할 때 적합
  * 장기적인 백업용 스토리지로 적합
* S3 One Zone-IA
  * 일반적으로 S3의 스토리지들은 최소 3개 이상의 가용 영역에 저장되지만 S3 One Zone-IA는 하나의 가용 영역에만 데이터를 저장
  * 하나의 가용 영역에만 저장하기 때문에 S3 Standard-IA에 비해 상대적으로 비용이 저렴
  * 비용은 상대적으로 저렴하나, 하나의 가용 영역에만 데이터가 저장되기 때문에 가용성이 떨어지게 된다는 단점. 따라서 가용성이 낮아도 큰 문제가 없는 데이터들을 S3 One Zone-IA에 저장하여 비용을 낮출 수 있음
* S3 Glacier / Deep Archive
  * S3 Glacier는 장기간 저비용 데이터 보관이 가능하며 주로 **아카이브** 목적으로 사용됩니다.
  * 데이터를 객체가 아닌 볼트(Vault)단위의 컨테이너로 저장
  * 다량의 데이터를 장기간 저장해야 할 경우에 적합


### S3 접근 관리

* S3에 접근하고자 하는 Principal에 Policy를 Custom하여 Attach할 때 유의점
```json
1. "Action": "ListAllMyBuckets"
2. "Action": "ListBucket"
```
* 위 1번은 계정 내 존재하는 버킷의 리스트를 조회하는 Action
  * `ls bucket` 
* 위 2번은 버킷 내 존재하는 객체(Object)의 리스트를 조회하는 Action
  * `ls object` 
* 따라서, 정책을 할당할 때 `ListAllMyBuckets`으로 버킷 리스트를 조회할 수 있도록 하고 `ListBucket` + 특정 bucket name을 통해 특정 버킷의 object들만 확인할 수 있도록 할당
  * `ListAllMyBuckets` 를 허용하지 않으면 `ListBucket` 를 모든 버킷에 허용해도 버킷 리스트 자체가 조회가 되지 않기 때문에 아무것도 볼 수 없다.