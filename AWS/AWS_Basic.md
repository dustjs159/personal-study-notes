💻 [AWS] AWS 기본 개념
=================
* AWS 서비스를 사용하기 전 기본적인 개념에 대한 요약

목차

* 글로벌한 AWS의 인프라 구조
  * Region
  * Availability Zone(AZ)
  * Edge location(pop)
* AWS의 서비스 레벨
* Service Endpoint
* ARN(Amazon Resource Name)

# 글로벌한 AWS의 인프라 구조
* Region : 데이터 센터의 집합
  * 리전마다 고유한 이름이 존재 
    * `ap-northeast-2` : 서울 리전
    * `us-east-1` : 버지니아 리전
  * 리전마다 서비스 비용이 조금씩 다름
  * 서비스를 이용할 고객의 위치에 따라 알맞게 배치하는 전략이 필요(Latency 최소화)
* Availability Zone(AZ) : 리전 내 데이터 센터를 논리적으로 나눠놓은 구역. 하나의 IDC라고 보면 된다.
  * 리전마다 AZ의 수가 다르다(서울은 4개)
    * `ap-northeast-2a` ~ `ap-northeast-2d` (a, b, c, d)
  * 위치가 정확히 어딘지는 모르지만 리전 내 서비스의 가용성을 위해 여분의 데이터 센터를 준비해둠
* Edge location (pop)
  * 사용자에게 더 빠르게 컨텐츠를 전송하기 위해 전 세계에 위치한 데이터 센터 : **CDN**
  * Cloudfront 정리할 때 자세히 다룰 예정.

# AWS의 서비스 레벨
* AWS의 서비스들은 크게 3 Level로 나눌 수 있다. 대부분의 AWS 서비스가 리전 수준이지만 일부는 글로벌한 수준의 서비스다. 
  * Global - IAM, Route 53, Cloudfront, WAF 등등..
  * Regional Level - EC2, VPC 등등 대부분.

# Service Endpoint
* API 사용시 접근하는 AWS 서비스의 Endpoint

```bash
protocol://service-code.region-code.amazonaws.com
```

* protocol : http or https
* service-code : AWS 서비스 고유의 코드. e.g. EC2, CloudWatch, S3 등
* region-code : region 별 고유 코드. e.g ap-northeast-2, us-east-2 등


# ARN(Amazon Resource Name)
* AWS 리소스들을 구별하기 위한 이름
```bash
arn:aws:service:region:account-id:resource-type:resource-id
```

* service : AWS 서비스 prefix
  * s3, iam 등등
* region : 리전 코드
  * ap-northeast-2(서울), us-east-1(버지니아) 등
* account id : AWS Account(사용자 아님!) ID
* resource-type : AWS 서비스 내 리소스
  * IAM 내의 Role이나 User, Policy같이 AWS 서비스 내 리소스들
* resource-id : AWS 서비스 내 리소스의 이름
  * IAM 내의 User의 이름 watson

