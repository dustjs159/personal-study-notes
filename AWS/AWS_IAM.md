Amazon IAM 
====================================
## Summary
- Last Updated : 21.09.01 Wed   
- Updated by : YEONSUN YOON
-----------------------------------

# 보안 3요소 - CIA
   
<img width="549" alt="스크린샷 2021-08-21 오전 4 30 47" src="https://user-images.githubusercontent.com/57285121/130284508-ec7bff78-1fab-497d-b629-4ac2cc9406f5.png">
   
* **기밀성(Confidentiality)** : 아무나 함부로 확인할 수 없고 **비밀스럽게 유지**되어야 하는 특성입니다. 허가받지 않은 사용자는 데이터에 접근이 불가능합니다. 만약 접근이 된다면 '기밀성이 깨졌다' 라고 합니다.
* **무결성(Intergrity)** : 아무나 정보를 **변형할 수 없도록 유지**해야 하는 특성입니다. 허가받지 않은 사용자는 데이터의 생성, 변경, 삭제가 불가능합니다. 만약 데이터 생성, 변경, 삭제가 된다면 '무결성이 깨졌다' 라고 합니다.
* **가용성(Availability)** : 서비스나 시스템이 **항상 장애 없이 가동**되어야 하는 특성입니다. 사용자는 원하는 날짜, 시간에 서비스나 시스템을 사용할 수 있어야 하고 만약 장애 발생으로 인해 사용하지 못하는 경우 '가용성이 깨졌다' 라고 합니다.

# 인증 & 인가
   
<img width="772" alt="스크린샷 2021-08-21 오전 4 33 33" src="https://user-images.githubusercontent.com/57285121/130284767-20a2e5aa-c7ab-4ce7-8f7d-0aa1c79608dd.png">
   
* 인증(Authentication) : 사용자가 **누구인지 확인**하는 절차입니다.   
> * Ex) 회사 건물에 출입할 때 사원증으로 인증을 통해 출입이 가능   
* 인가(Authorization) : 사용자의 **요청에 대한 권한을 확인**하는 절차입니다.   
> * Ex) 회사 건물에는 들어올 수 있으나 들어와서 특정 사무실에는 출입이 불가(관계자 외 출입금지)   

# AWS를 이용하는 방법
1. AWS 웹 관리 콘솔
   
<img width="715" alt="스크린샷 2021-08-22 오전 1 12 46" src="https://user-images.githubusercontent.com/57285121/130328117-2f6be0c6-fe36-4a3b-9f8b-d5307db9c42a.png">
   
> * AWS 계정으로 웹 관리 콘솔에서 리소스를 관리하는 방법입니다. 쉽고 직관적으로 생성할 수 있다는 장점이 있지만 하나씩 클릭하며 생성해야 하기 때문에 시간이 오래걸리며 반복 작업에 적합하지 않다는 단점이 있습니다.   

2. CLI(Command Line Interface) & Script
   
<img width="711" alt="스크린샷 2021-08-22 오전 1 16 51" src="https://user-images.githubusercontent.com/57285121/130328259-61249b43-6a10-4c3c-837c-00aff9e46b81.png">
   
> * AWS Shell과 스크립트를 사용하여 리소스를 관리하는 방법입니다. 스크립트를 활용한 반복 작업과 재사용이 용이하다는 장점이 있지만 동시에 다수의 사용자가 스크립트를 실행할 경우 문제가 발생할 수 있고 복원이 어렵다는 단점이 있습니다.   

3. AWS CloudFormation
   
<img width="710" alt="스크린샷 2021-08-22 오전 2 38 14" src="https://user-images.githubusercontent.com/57285121/130330444-d6fd4484-723f-4f9f-af31-ee20250f71d1.png">
   
> * CloudFormation Template(JSON 혹은YAML 형식의 파일)으로 리소스를 관리합니다. 자동화 구현에 용이하며 에러 발생 시 복구가 쉽다는 장점이 있지만 구현하기 위한 언어를 별도로 숙지하고 있어야합니다.   

4. SDK - AWS CDK
   
<img width="726" alt="스크린샷 2021-08-22 오전 2 46 10" src="https://user-images.githubusercontent.com/57285121/130330677-0a801318-c4c1-465e-bc93-fa029274163a.png">
   
> * AWS CDK(Cloud Development Kit)을 사용하여 리소스를 관리합니다. 익숙한 프로그래밍 언어를 사용하여 인프라를 코드로 정의합니다. 별도의 언어를 숙지할 필요가 없습니다.   

### ***AWS 리소스를 생성, 접근, 관리하기 위해서는 API를 사용***

# AWS IAM
   
<img width="716" alt="스크린샷 2021-08-26 오전 12 06 31" src="https://user-images.githubusercontent.com/57285121/130816065-d7312455-a14c-4720-873c-bcd9b0394d1a.png">
   
* AWS Identify Access Management(IAM) : AWS 전체의 권한 통제 시스템
* AWS에서는 대부분 리소스들간 **API**를 사용하여 접근 및 제어를 합니다. 이 때 **인증(Identity)** 과 **인가(Access Management)** 를 통해 리소스에 대한 접근을 제한합니다.

# 보안 주체(Principal)
보안 주체는 AWS리소스에 대해 액세스하고 작업을 수행할 수 있는 사람 또는 객체를 말합니다. 보안 주체는 AWS 계정 root 사용자 혹은 IAM 자격 인증을 통해 인증 절차를 수행하고 AWS에 요청합니다.
모든 보안 주체는 AWS에 API로 요청을 할 때 Access Key + SecretKey로 구성된 Credential을 포함하여 인증을 받게 됩니다.
   
* root User / IAM User
* IAM Group
* IAM Role
   
<img width="305" alt="스크린샷 2021-08-22 오전 12 36 36" src="https://user-images.githubusercontent.com/57285121/130327106-17f9acf4-1413-4eac-af8b-c83454a47f42.png">
   
## root User
   
<img width="521" alt="스크린샷 2021-08-22 오전 12 54 13" src="https://user-images.githubusercontent.com/57285121/130327612-8d611b62-0f45-4319-ba59-70139c91b51f.png">
   
* AWS에 회원가입을 하게 되면 계정이 생성됩니다. 이 때 사용한 이메일 주소와 비밀번호를 **root 계정 자격 증명**이라고 합니다. 이메일 주소와 비밀번호를 입력하면 AWS 웹 관리 콘솔에 로그인 할 수 있습니다.
* root 사용자는 AWS 계정의 **모든 리소스들에 대해 자유롭게 접근이 가능**합니다. 뿐만 아니라 결제 정보와 비밀번호까지 변경할 수 있습니다. 
* 하지만 특별한 경우가 아니라면 보안상 root 사용자로 리소스에 접근 하는 것은 좋지 않기 때문에 피하도록 합니다.(첫 번째 계정을 생성할 때, IAM 사용자를 생성할 때 이외에는 미사용)

## IAM User
   
<img width="488" alt="스크린샷 2021-08-22 오전 1 03 10" src="https://user-images.githubusercontent.com/57285121/130327844-efcd8a24-73a3-4651-95b0-f2a24beee906.png">
   
* AWS IAM의 자격 증명을 통해 사용자의 **인증**을 받은 계정입니다.
* 기본적으로 사용자는 계정 내 어떠한 리소스에도 접근할 수 없습니다. **IAM의 인증을 거쳐 리소스 접근에 대한 권한을 부여받아 접근**할 수 있습니다.
* IAM 사용자는 장기적인 Credential(AccessKey + SecretKey), 즉 **상시 자격증명**을 통해 AWS 리소스에 접근합니다.
* IAM 사용자는 실제 사용자와 1:1로 매핑되어야 하고 주기적으로 자격 증명을 교체해주어야 합니다.(사용자의 자격 증명이 영구적으로 유지되기 때문)
* IAM 사용자를 생성할 때 AWS 액세스 유형을 선택할 수 있습니다.
   
<img width="783" alt="스크린샷 2021-08-23 오후 4 08 01" src="https://user-images.githubusercontent.com/57285121/130405073-e59bc634-85c2-4664-8a4f-dbeae4b03ef4.png">
   
> * 프로그래밍 방식 : AWS API, CLI 등을 통해 접근할 수 있는 액세스 키를 생성하여 AWS 리소스에 접근할 수 있습니다.   
> * AWS 웹 관리 콘솔 방식 : AWS 웹 관리 콘솔을 통해 로그인할 수 있는 비밀번호를 설정하여 리소스에 접근할 수 있습니다.   

## IAM Group
   
<img width="362" alt="스크린샷 2021-08-23 오후 7 02 35" src="https://user-images.githubusercontent.com/57285121/130429162-7ffee325-e145-445c-933d-e6999a9f49bf.png">
   
* IAM 그룹은 IAM User들의 집합입니다. 그룹명을 지정하고 사용자를 추가하여 사용자 모음을 만들 수 있습니다.

## IAM Role
   
<img width="685" alt="스크린샷 2021-08-23 오후 5 44 38" src="https://user-images.githubusercontent.com/57285121/130417907-9c2e2474-03f3-4fa5-a571-5b08fa7bd16d.png">
   
* IAM 역할은 **IAM 자격 증명**입니다. 
* IAM 사용자와 마찬가지로 IAM 자격 증명이지만 IAM 사용자 한 명에게만 국한된 것이 아니라 외부 사용자에게도 역할을 부여해 IAM 자격 증명을 수행할 수 있습니다.
* IAM 역할은 IAM 사용자의 장기적인 Credential이 아닌 자동으로 로테이션되는 임시 Credential을 사용합니다. 여기서 임시 Credential은 AccessKey + SecretKey와 추가적으로 일정 시간이 지나면 만료되는 Token이 발급되는 형태입니다. 이 역할을 **Assume Role**이라고 합니다.
* IAM 사용자의 장기 Credential을 영구적으로 코드에 직접적으로 사용하게되면 위험하기 때문에 Assume Role을 사용하는 것이 보안상 더 안전합니다.

# IAM Policy
   
<img width="377" alt="스크린샷 2021-08-26 오전 1 53 40" src="https://user-images.githubusercontent.com/57285121/130832662-455e7442-424b-4b1b-9dfa-76f3fe11bf46.png">
   
* IAM 정책이란 AWS 서비스와 리소스에 대해 수행할 수 있는 **작업의 허용/거부 규칙**입니다.
* 정책을 정의할 때는 어떤 IAM 이 어떤 상태(Condition)에서 AWS의 어떤 리소스에 대해 **어떤 작업(Action)을 허용 혹은 차단할지 지정**합니다. 정의된 정채을 바탕으로 API 요청을 검사, 평가하게 되어 특정 리소스에 대한 작업을 허용할지 차단할지 결정합니다.
* 정책은 default값이 `Deny`이며 `Allow`보다 `Deny`의 우선순위가 높습니다.
* 대부분의 정책은 AWS에 **JSON 문서로 저장**됩니다.

## IAM 정책 유형

**자격 증명 기반(Identity-based) 정책** 
* 자격 증명 기반 정책은 IAM 보안 주체(User, Group, Role)에 할당되어 해당 보안 주체의 권한을 규정합니다.(Policy가 ID에 할당)
* 정의 및 관리 : IAM / 포맷 : JSON
* 자격 증명 기반 정책의 분류는 AWS 관리형 정책과 인라인 정책이 있습니다.
* 관리형 정책 : AWS 계정 내 속한 다수의 사용자, 그룹에게 연결할 수 있는 정책입니다. 관리형 정책에는 AWS에서 생성하고 관리하는 정책과 사용자가 자신의 AWS 계정에서 생성하고 관리하는 정책 두 유형이 있습니다.   
> * AWS 관리형 정책 : **AWS에서 생성 및 관리**하는 독립적인 정책입니다. 보다 일반적인 사례에서 사용하기 적합하며 청구, DB관리자, 네트워크 관리자 등 직무에 따른 관리형 정책을 통해 보다 수월하게 업무에 적용할 수 있는 정책을 생성할 수 있습니다.
   
<img width="462" alt="스크린샷 2021-08-26 오후 2 53 54" src="https://user-images.githubusercontent.com/57285121/130908509-432d2aa1-65b7-4acb-afee-2364130c0e7c.png">
   
<img width="465" alt="스크린샷 2021-08-26 오후 3 07 24" src="https://user-images.githubusercontent.com/57285121/130909927-bf90925f-553d-490f-ae24-e9023f1644c3.png">
   
> * 고객 관리형 정책 : : 사용자가 직접 자신의 AWS 계정에서 생성하고 관리하는 정책입니다. 자유롭게 정책을 커스터마이징할 수 있습니다.   

* 인라인 정책 : 단일 사용자, 그룹, 역할에 직접 추가하는 정책입니다. 정책과 ID가 1:1관계로 유지됩니다. ID 삭제 시 인라인 정책도 함께 삭제됩니다.
   
**리소스 기반(Resource-based) 정책**
* 리소스 기반 정책은 리소스를 기준으로 보안 주체의 작업에 대해 허용/거부할 권한을 규정합니다.(Policy가 Resource에 할당)
* 정의 및 관리 : 개별 리소스들 / 포맷 : JSON

### Identity / Resource based Policy
   
<img width="452" alt="스크린샷 2021-08-26 오후 3 50 17" src="https://user-images.githubusercontent.com/57285121/130914950-a054faa5-53a2-4fdd-b6bd-25b4c4749dc4.png">
   
* Identity-based Policy : **요청하는 주체에게 연결**되는 정책(접근을 **하기 위한** 정책)
* Resource-based Policy : **요청을 받는 리소스에 연결**되는 정책(접근을 **받기 위한** 정책)
* Resource-based 정책에는 ``Principal`` 구문(보안 주체)이 추가됨
   
<img width="163" alt="스크린샷 2021-08-26 오후 3 54 21" src="https://user-images.githubusercontent.com/57285121/130915498-d39b7df1-50b1-4516-b10a-ce2c95b52028.png">
   
* 보안 주체와 리소스 둘 다 정책이 있다면 정책의 내용이 겹치게 될 수 밖에 없는데 이 때 요청 권한 검사를 할 경우 동일 계정(In-Account)환경에서는 **두 정책의 합집합**을 검사하며
   
<img width="176" alt="스크린샷 2021-08-26 오후 3 54 44" src="https://user-images.githubusercontent.com/57285121/130915565-1851588f-5a1c-47de-bcd2-53e3fc498041.png">
   
* 다른 계정(Cross-Account)환경에서는 **두 정책의 교집합**을 검사합니다.(이 때 `Deny` 우선 적용)

IAM 권한 경계(IAM Permission Boundary) 정책
* IAM 보안 주체별로 획득할 수 있는 최대의 권한을 규정합니다.
* 정의 및 관리 : IAM / 포맷 : JSON
   
서비스 제어(Organization SCP) 정책
* 기업이 소유하는 AWS 계정을 그룹화하고 중앙에서 관리합니다. AWS 계정 내 각 계정의 권한을 단일/그룹별로 제어할 수 있습니다.(중앙 집중식 관리)
* 정의 및 관리 : 기업 및 조직 / 포맷 : JSON

세션(Session) 정책
* 특정 세션에 대해 임시 보안 자격 증명을 적용합니다.
* 정의 및 관리 : AWS STS(Security Token Service) / 포맷 : JSON

## 정책의 JSON 구조
``` json
{
"Version" : "2021-08-26",
"Statement" : [
	{
	"Effect":"Allow or Deny",
	"Principal":"principal",
	"Action":[
		...
			],
	"Resource":[
		...
			],
	"Condition":{
		...
			}
		}	
	]
}
```
- `Effect` : 허용(Allow) or 차단(Deny)
- `Principal` : 접근을 허용 or 차단하고자 하는 대상(보안 주체)
- `Action` : 리소스에 대한 작업(형식 : [서비스명]:[작업명]. Ex, s3:GetObject)
- `Resource` : 서비스에 대한 리소스들의 상세 조건. ARN(Amazon Resource Number)사용
- `Condition` : 어떤 조건에서

### ARN(Amazon Resource Number)
* AWS 리소스들을 고유하게 식별하기 위한 **구분자**
* 형식
``arn:partition:service:region:account-id:resource-type:resource-id``   
> * ``partition`` : 리소스가 위치한 AWS 리전의 그룹. `aws` : AWS 리전, `aws-cn-` : 중국 리전)   
> * ``service`` : 서비스의 고유한 서비스 접두사. `s3`, `iam`, `ec2` 등   
> * ``region`` : 리전 코드   
> * ``account-id`` : 계정 번호   
> * ``resource-type`` & ``resource-id`` : 리소스의 경로   

## API 요청이 성공하기 위해서는
### 1. IAM 보안주체(IAM User / Group / Role)가 적절한 Credential을 통한 **인증**과
### 2. 정책(Policy)에 의해 작업을 수행하기 위한 API 요청이 적절한 규칙에 따라 **인가**되어야 함


