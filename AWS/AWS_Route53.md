💻 [AWS] AWS Route53
===============
# 💡 AWS Route53

* AWS의 DNS 서비스
* 웹서버의 IP와 도메인 이름을 매핑
  * 도메인의 A Record에 웹 서버 IP 등록
* 서비스의 엔드포인트와 도메인 이름을 매핑
  * 도메인의 CNAME Record에 Endpoint 등록

## 📌 Route 53 주요 기능

* 도메인 등록 & 트래픽 라우팅
* Health Check
* ACM(AWS Certificate Manager)에서 생성 및 관리하는 인증서가 포함된 도메인 등록을 통해 HTTPS 가 적용된 도메인 사용

## 📌 Route 53 동작 원리

<img width="579" alt="스크린샷 2022-06-14 오후 11 13 27" src="https://user-images.githubusercontent.com/57285121/173598824-b52d29fa-e0bd-41f0-b7bd-fb3fc16ee728.png">

* 일반적인 DNS 동작 원리와 동일하나 Public Zone / Private Zone에 대한 이해가 필요
* 계층적 구조
  * Root DNS > TLD DNS > Route 53 순서로 쿼리

## 📌 Route 53 호스팅 영역

* 호스팅 영역은 **Public Zone** or **Private Zone** 으로 나누어져 있음 
* 각 Zone에는 다음과 같은 정보가 매핑되어 있는 Zone File이 포함되어 있음
  * 도메인
  * 리소스(IP Address, ALB DNS Name, CloudFront Distribution, API Gateway 등)
  * DNS Record
* Public Zone
  * DNS 쿼리에 응답하는 DNS Name Server가 누구나 접근 가능한 인터넷 상에 있음
  * 즉, 외부에서 해당 도메인을 쿼리하면 Public IP 가 나옴
    * `nslookup` 커맨드로 도메인 쿼리 시 Public IP
* Private Zone
  * DNS 쿼리에 응답하는 DNS Name Server가 VPC 내부에 있음
  * VPC 내 호스트가 특정 도메인을 쿼리했을 때 가장 먼저 Private Zone의 DNS 서버에 쿼리하게 되며 쿼리한 도메인의 정보가 DNS 서버 내 Zone File에 있는 정보일 경우 VPC 외부에 다시 쿼리하지 않고 해당 Zone File의 정보를 반환
* TTL(Time To Live)

## 📌 호스팅 영역에 다른 VPC를 연결하는 방법
* AWS CLI 사용해야 함
