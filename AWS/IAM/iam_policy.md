💻 [AWS] IAM Policy
=================

# IAM Policy
* Principal의 Request를 허용(Allow)할지 거부(Deny)할지 결정
* JSON Format
* Policy 종류
  * Identity-based Policy
  * Resource-based Policy
  * Permission Boundary
  * SCP
  * Session Policy

### Policy 구조
``` json
{
"Version" : "2012-10-17",
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
* `Version` : 정책의 언어 버전. 버전이 예전 버전으로 명시되어 있을 경우 특정 변수에 대해서 변수가 아닌 문자열로 인식할 수도 있음.
    * latest : `2012-10-17`
* `Id`
* `Statement`
    * `Sid` : String ID.
    * `Effect` : 허용(Allow) or 차단(Deny)
    * `Principal` : 접근을 허용 or 차단하고자 하는 대상(보안 주체)
        * **Resource 기반 정책에서 필수로 작성**
    * `Action` : 리소스에 대한 작업(형식 : [서비스명]:[작업명]. e.g. s3:GetObject)
    * `Resource` : 서비스에 대한 리소스들의 상세 조건. ARN format 사용
    * `Condition` : 어떤 조건에서

# 정책 적용 우선 순위
* policy 적용 우선 순위
* **Deny**

# AWS 계정을 보다 안전하게
* Password 정책 설정
* MFA 설정하기
* IP 제어하기