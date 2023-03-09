💻 [AWS] AWS IAM
=================
* AWS IAM(Identity & Access Management) : **AWS 내 서비스에 대한 접근 제어 서비스**
* **모든 요청은 API 호출이다.**
  * AWS 콘솔이나 CDK or SDK를 통해 AWS 자원에 접근하는 행위는 모두 API 호출!
  * 따라서 AWS IAM 서비스는 사용자의 API 호출에 대해 접근 제어하는 서비스. 
* 글로벌 서비스

목차

* 인증 & 인가
* Root 계정 (Account)
* IAM 동작 원리
* IAM 리소스
  * 사용자 - User
  * 그룹 - Group
  * 정책 - Policy
  * 역할 - Role

# 인증 & 인가
IAM을 사용하기 전, 인증과 인가에 대한 개념을 짚고 넘어가도록 하자.
![](https://images.velog.io/images/dustjs159/post/d0ce58f3-cd3f-4145-92f6-4428175ce225/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-03-20%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%205.32.06.png)

* 인증(Authentication) : Who Are You?
  * 사용자가 누구인지 확인하는 절차
  * e.g. 회사 건물에 출입할 때 사원증 or 지문 등으로 출입하려는 자가 누구인지 확인
* 인가(Authorization) : Are you allowed to do that?
  * 사용자의 특정 행위에 대한 제어
  * e.g. 인증 절차를 통과한 후에 건물 출입은 가능하나 특정 사무실에는 출입할 수 없음
* **한국어로써 인증과 인가의 단어가 주는 느낌은 비슷할 수 있으나, 영어로 번역된 Authentication(인증)과 Authorization(인가)는 엄연히 다른 의미이므로 주의!**

# Root 계정 (Account)
* Root Account : AWS에 회원 가입 후 최초에 로그인하게 되는 계정
  * Root Account는 너무 많은 권한을 갖고 있기에 **최초 로그인하는 경우와 첫 IAM User 를 생성하는 경우를 제외하면 사용하지 않는다.** (그냥 무조건 쓰지 마)
  * 고유한 Account ID (혹은 Owner ID)를 가지고 있음
  * Account 내에 여러 서비스를 셍성하고 다른 Account간에 접근이 불가능 
  * 조직 내에서 Root Account로 Admin User를 생성하고 Admin User로 여러 다른 계정을 만들어서 관리 

# IAM 동작 원리
동작 원리

![스크린샷 2022-07-22 오전 12 40 19](https://user-images.githubusercontent.com/57285121/180255247-457ac69f-6a2b-4171-8ef4-a371b7c1ad7f.png)

* IAM의 접근 제어는 인증과 인가로 수행
  * 인증(Authentication): IAM 서비스를 통해 AWS 웹 콘솔에 로그인(Sign in)
    * AWS 콘솔 로그인 : ID + Password + MFA Token(Optional)
    * API 호출 : Access Key + Secret Access key + MFA Token(Optional)
  * 인가(Authorization) : 로그인 한 사용자에 대해 서비스와 리소스 접근 권한 제어(Permission Control)

# IAM 리소스 
* IAM Resource : User, Group, Role, Policy
  * 다른 AWS 서비스들과 마찬가지로 생성, 변경, 삭제 가능
* IAM Entities : User, Role
  * IAM 리소스 중 AWS에 로그인(= Sign in)할 때 인증(Authentication)의 대상
  * 로그인 할 때 Group은 물어보지 않으므로 Group은 제외
* IAM Identities : User, Group, Role
  * IAM 리소스 중 정책을 통해 권한을 부여받을 수 있는(Authorization) 대상
* Principal
  * 보안 주체. AWS에 무언가를 Request하는 주체
  * AWS 웹 콘솔에서 클릭(Action)하는 User
  * AWS API를 호출하는 User or APP

## 사용자 - User
* User : AWS로 요청을 하고 그에 대한 응답을 받는 Principal

![](https://images.velog.io/images/dustjs159/post/1a5b4f40-5196-41b1-b61e-b25c47ae3707/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-03-22%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%2012.14.36.png)

* 이 때 각 IAM User들에게 부여되는 권한은 최소 권한 부여 원칙에 의해 최소한의 권한만을 부여하는 것이 모범사례.
### Federated User

![](https://images.velog.io/images/dustjs159/post/8fc3524d-ac59-4289-a316-16aeb4a90fac/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-03-22%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%2012.20.22.png)

* 외부 조직에서도 AWS 계정 내 리소스에 접근이 가능함
* 임시 자격 증명을 통해 접근 권한을 얻을 수 있음(영구적인 권한 X)

## 그룹 - Group
* 동일한 Policy 의 적용을 받는 User들의 집합
* 인증 대상은 아님(로그인 할 때 Group을 물어보지는 않으므로)
* User당 속할 수 있는 Group의 수는 10개

## 정책 - Policy
* Principal의 Request를 허용(Allow)할지 거부(Deny)할지 결정
* JSON Format
* Policy 종류
  * Identity-based Policy
  * Resource-based Policy
  * Permission Boundary
  * SCP
  * Session Policy

## 역할 -  Role
* 특정 권한을 갖는 IAM Identity
* user가 아닌 principal에 대한 권한.

