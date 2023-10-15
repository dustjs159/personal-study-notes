Terraform 변수 다루기
=====================
### 사용 가능한 변수
* string
* number
* bool
* list
* set
* map
* object
* tuple
* input
* output

### terraform console에서 변수 확인
```bash
$ terraform console
> var.varname
> "${var.varname}" 
```

#### string
* 문자열
```
variable mystr {
  type        = string
  default     = "string variable"
}
```

#### number
* 정수형(실수도 가능)
```
variable mynumber {
  type        = number
  default     = 3.14
}
```

#### list
* 리스트
* 인덱싱은 0부터.
* `element()`, `slice()` 등으로 리스트 내 요소 추출 가능
```
variable mylist {
  type        = list
  default     = [1,"string1",3]
}
```

#### map
* key-value 형태로 데이터 저장 가능 (파이썬으로 치자면 딕셔너리)
```
variable mymap {
  type        = map(string)
  default     = {
    key1 = "value1"
    key2 = "value2"
  }
}
```
* `"${var.mymap["key1"]}"` 형태로 사용


 ### 변수 관리 
 * 변수 재사용을 위해 별도의 변수 지정 파일을 생성하고 외부에서 변수를 사용할 때 해당 파일을 참조하여 변수를 사용.
    * `variables.tf`, `terraform.tfvars` 를 통해 관리

### variables.tf vs terraform.tfvars
* `variables.tf` : **변수의 placeholder**
    * 변수의 이름과 type을 **선언**하는 파일. description도 작성 가능.
```
variable "aws_region" {
  type        = string
}
variable "availabilty_zones" {
  type        = list
}
variable "ami_id" {
  type        = map
}
```
* `terraform.tfvars` : `variables.tf` 파일에서 선언한 **변수의 placeholder에 실제로 들어갈 값**
  * 변수 타입에 관계없이 저장 가능.
```
aws_region = "ap-northeast-2"
availabilty_zones = ["ap-northeast-2a", "ap-northeast-2b", "ap-northeast-2c", "ap-northeast-2d"]
ami_id = {
    ami_amd = "ami-11111"
    ami_arm = "ami-22222"
}
```

### Variables Naming Conventions
* 소문자로 작성한다.
  * `region` (O), `REGION` (x)
* 하이픈(-) 이아닌 언더바(_)를 사용한다.
  * `aws_region` (O), `aws-region` (x)
* 참조 링크 : https://www.terraform-best-practices.com/naming