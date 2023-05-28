💻 [AWS] IAM Policy
=================
* IAM Policy
	* Principal의 Action에 대해 허용(Allow)할지 거부(Deny)할지 결정하는 JSON 형태의 문서
	* 정책을 직접 만들어서 사용할 수도 있고(Custom) Amazon이 만들어둔 정책을 사용할 수도 있음
	* 정책 부여 대상은 사용자, 그룹, Role, Resource 등이 될 수 있음
* Policy 종류
	* Identity-based Policy
	* Resource-based Policy
	* Permission Boundary
	* SCP
	* Session Policy

# Policy 구조
``` json
{
"Version" : "2012-10-17",
"Id" : "S3 Permission",
"Statement" : [
	{
	"Sid" : "1",
	"Effect" : "Allow or Deny",
	"Principal" : "principal",
	"Action" : [
		...
			],
	"Resource" : [
		...
			],
	"Condition" : {
		...
			}
		}	
	]
}
```
* `Version` : 정책의 언어 버전. 버전이 예전 버전으로 명시되어 있을 경우 특정 변수에 대해서 변수가 아닌 문자열로 인식할 수도 있음.
    * latest : `2012-10-17`
* `Id` : 정책 전체에 대한 구분자.
* `Statement`
    * `Sid` : String ID. "Statement"에 대한 구분자.
    * `Effect` : 허용(Allow) or 차단(Deny)
    * `Principal` : 접근을 허용 or 차단하고자 하는 대상(보안 주체)
        * Account, Role, User 등의 주체를 ARN 형태로 작성
		* **Resource 기반 정책에서 필수로 작성**
    * `Action` : 리소스에 대한 작업
		* 형식 : [서비스명]:[작업명]. e.g. s3:GetObject
    * `Resource` : 서비스에 대한 리소스들의 상세 조건. ARN format 사용
    * `Condition` : 위 정책을 적용하기 위한 특정 조건

# 정책 적용 우선 순위
* 여러 정책들이 있을 때, 정책 적용 우선 순위는 명시적 **Deny**가 가장 먼저 적용된다.
	* 명시적 Deny > 암묵적 Deny > 명시적 Allow
		* 허용되지 않은 Action에 대해서는 모두 Deny.

# AWS 계정을 보다 안전하게
* Password 정책 설정
	* 특수문자/대문자 포함, 길이 설정, 유효기간 설정 등
* MFA 설정하기
	* IAM 정책으로 MFA 설정이 되어있지 않은 사용자는 접근 제한 설정 가능
* IP 제어하기
	* 특정 IP 이외는 모두 접근 차단하여 보다 안전하게 계정 관리 가능
		* 다만 Public IP에 대해서만 접근 제어할 수 있고 Private IP에 대해서는 접근 제한할 수 없음.