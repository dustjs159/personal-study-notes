💻 [AWS] AWS Route53
===============
# 💡 AWS Route53

* AWS의 DNS 서비스
* 웹서버의 IP와 도메인 이름을 매핑
  * 도메인의 A Record에 웹 서버 IP 등록
* 서비스의 엔드포인트와 도메인 이름을 매핑
  * 도메인의 CNAME Record에 Endpoint 등록


## 📌 Route 53 주요 기능

* 도메인 등록
* DNS Routing
* Health Check

## 📌 Route 53 도메인 등록 과정
* 도메인 등록
  * 도메인 이름과 같은 이름의 Hostzone 생성
  * **Public** or **Private** 선택
* Public Zone : 외부에서 사용 가능
* Private Zone : VPC 내부에서만 사용 가능

