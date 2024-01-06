Terraform Remote State Management
=====================
### 테라폼의 state 관리
* 테라폼은 인프라 구조의 상태를 원격으로 관리한다.
* `terraform apply` 시점에 아래와 같은 파일이 생성된다. 
    * `terraform.tfstate` : 현재 인프라 구조의 상태가 저장되어 있는 파일
    * `terraform.tfstate.backup` : 이전 인프라 구조의 상태에 대한 백업본

### backend 기능을 활용한 원격 제어
* backend 기능을 활용하여 원격 저장소에 상태를 저장하고 관리할 수 있음.
    * s3 bucket, terraform consul 등에 원격 상태 저장 가능

s3 bucket에 backend 기능을 활용하여 원격 상태를 저장하는 방법
```
# backend.tf
terraform {
    backend "s3" { 
      bucket         = "terraform-infra-s3-bucket" # s3 bucket 이름
      key            = "project-terraform.tfstate" # s3 bucket 내 저장 경로
      region         = "ap-northeast-2"  
      encrypt        = true
    }
}
```

### .tfstate 파일이 제거될 경우
* 테라폼이 원격 상태를 알 수 없으므로 `terraform.tfstate` 파일을 수동으로 다시 생성해야 한다.

### 두 명 이상의 작업자가 `terraform apply` 한 경우