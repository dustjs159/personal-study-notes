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