Go Language 
=============

# Basic

### Package
```go
package main
```

* Package Name : 프로젝트 내에서 컴파일 할 코드에 작성
  * 컴파일러는 Package 명이 `main` 인 것을 먼저 찾고 컴파일 함
  * `main` 이 아니라면 컴파일 안 됨
    * 라이브러리, 오픈소스 공유 용도의 코드들은 Package 이름에 `main` 을 사용하지 않음


### Main Function

```go
func main() {

}
```

* Main Function : 컴파일러가 가장 먼저 찾는 함수
* Go Compiler는 Main Package 내의 Main Function 을 가장 먼저 찾아 실행!

### Import

```go
import (

) 
```
* import할 패키지 목록
* 그 중에서 패키지 내에 대문자로 시작하는 함수는 **Public**. 패키지 import해서 해당 함수를 사용할 수 있음
* 소문자로 시작하는 함수는 **Private**. 패키지 import해서 함수 사용 불가

### 상수(Constant) & 변수(Variable)

```go
const name string = "who"
var a int = 755 
a := 7 // 축약형
```
* 상수 & 변수 둘 다 `Type` (`int`, `string` .... 등) 지정
* `const` : 변하지 않는 값
* `var` : 변하는 값.
* `Type` 을 생략하는 축약형도 사용 가능
  * `Type` 을 알아서 지정해줌. 대신 축약형으로 작성한 변수의 `Type` 은 바꿀 수 없음
  * 축약형은 `func()` 밖에서 사용 불가하며 **변수**에만 사용 가능

