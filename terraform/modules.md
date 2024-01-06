Terraform Modules
=====================
### 테라폼의 모듈
* 코드를 조각화하여 재사용 가능한 코드
* 공통적으로 사용하는 코드(보통 VPC 설정 같은) 재사용성 UP
* 테라폼의 진입점이 되는 곳이 Root Module이 되며 하위 `modules` 내 경로가 Child Moudle이 된다.
```
# main.tf (진입점)
module "vpc" {
  source = "./modules/vpc"
}
```