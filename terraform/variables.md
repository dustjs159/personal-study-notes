Terraform Variable Management
=====================
### 사용 가능한 변수
* 단순 변수
  * string
  * number
  * bool
* 복합 변수 
  * list
  * set
  * map
  * object
  * tuple
* input
* output

### terraform console에서 변수 확인
```shell
$ terraform console
> var.varname
# 또는
> "${var.varname}" 
```

### string
* 문자열
```
variable mystr {
  type        = string
  default     = "string variable"
}
```

### map
* key-value 형태로 데이터 저장 가능 (파이썬의 딕셔너리와 유사)
```
variable mymap {
  type        = map(string)
  default     = {
    "key1" = "value1"
    "key2" = "value2"
  }
}
```
```shell
$ terraform console
> "${var.mymap["key1"]}"
> lookup(var.mymap, "key1") # lookup 함수를 사용하여 변수 참조
```
### list
* 리스트 (파이썬의 리스트와 유사)
  * 인덱싱은 0부터.
* `element()`, `slice()` 등으로 리스트 내 요소 추출 가능
```
variable mylist {
  type        = list
  default     = [ 1, "string1", 3 ]
}
```

### set
* list와 유사하나 중복값에 대해 하나의 값만, 작은 요소부터 출력
  * 내부 요소들의 순서를 보장해주지는 않음.
* 단, type을 지정해주지 않으면 오류 발생.
  * `set(any)`로 지정 시 오류 발생하지 않음. 그러나 지정하는 것을 권고
```
variable mylist {
  type        = set(any) # 형식을 지정해줘야 함.
  default     = [ 1, "string1", 3 ]
}
```

### number
* 정수형(실수도 가능)
```
variable mynumber {
  type        = number
  default     = 3.14
}
```

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

### 변수 입력 받기
* 변수 선언 시 default 값을 지정하지 않으면, `terraform apply` 시점에서 입력받을 수 있음.
* 대화식이 아닌 선언식으로 변수를 입력할 때는 `-var <variable>` 형식으로 사용
  * `terraform apply -var <variable>`

### 출력 변수 설정하기 
* 생성한 리소스의 특정 정보를 출력 변수로 뽑아내고 싶을 때 사용하도록 한다.

```
output "<NAME>" {
    value = <VALUE>
    [CONFIG...]
}
```