💻 [AWS] AWS Basic
=================
# 💡 AWS 기본 개념
* AWS 서비스를 사용하기 전 기본적인 Concept에 대한 요약
* 목차
  * 루트 계정(Root Account)과 일반 사용자(IAM User)
  * 리젼(Region) & 가용영역(Availability Zone)
  * Service Endpoint
  * ARN(Amazon Resource Name)

## 📌 Root Account & IAM User
* Root Account : AWS에 회원 가입 후 최초에 로그인하게 되는 계정
<img width="319" alt="스크린샷 2022-05-29 오후 6 20 20" src="https://user-images.githubusercontent.com/57285121/170861140-3fabad14-196a-4615-91f9-1b641d342936.png">
  * Root Account는 너무 많은 권한을 갖고 있기에 최초 로그인하는 경우와 최초의 IAM User 를 생성하는 경우를 제외하면 사용하지 않는 것을 권고
  * 고유한 Account ID (혹은 Owner ID)를 가지고 있음
  * Account 내에 여러 서비스를 셍성하고 다른 Account간에 접근이 불가능 

* IAM User
  * Account 내에 생성되는 여러 계정
  * 조직 내에서 Root Account로 Admin User를 생성하고 Admin User로 여러 다른 계정을 만들어서 관리
  * 이 때 각 IAM User들에게 부여되는 권한은 최소 권한 부여 원칙에 의해 최소한의 권한만을 부여한다

## 📌 Region & Availability Zone
* Region : 물리적인 데이터 센터가 위치한 지역
* Availability Zone(AZ) : 리전 내 물리적 데이터 센터를 논리적으로 나눠놓은 구역 
  * 리전마다 AZ의 수가 다르다(서울은 4개)
  * 가용성을 보장하기 위함
* AWS의 서비스들은 크게 3 Level로 나눌 수 있다. 각 Level마다 서비스들이 생성되는 위치가 다름
  * Global
  * Regional Level
  * AZ Level

## 📌 Service Endpoint
* API 사용시 접근하는 AWS 서비스 자체의 Endpoint

`protocol://service-code.region-code.amazonaws.com`
  * protocol : http or https
  * service-code : AWS 서비스 고유의 코드. e.g. EC2, CloudWatch, S3 등
  * region-code : region 별 고유 코드. e.g ap-northeast-2, us-east-2 등


## 📌 ARN(Amazon Resource Name)


