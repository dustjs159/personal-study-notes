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

### 변수 확인
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
* key-value 형태로 데이터 저장 가능 (파이썬으로 치자면 유사 딕셔너리)
```
variable mymap {
  type        = map(string)
  default     = {
    key1 = "value1"
    key2 = "value2"
  }
}
```
 