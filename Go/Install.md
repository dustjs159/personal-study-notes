Go Language
===============

* VScode에서 Golang 개발 환경 세팅
* AWS SDK for Go 세팅

## Golang 개발 환경 세팅

* MacOS 에서 진행

* golang 설치
  * URL : https://golang.org/

* VScode 설치
  * URL : https://code.visualstudio.com/Download/
  * Go Extension 설치

* 프로젝트 디렉토리 설정
  * golang을 설치하면 `/usr/local/go` 가 생성이 될 것
    * `$ go env` 로 go 환경변수 조회가 되면 성공적인 설치가 된 것
    * 별도의 `~/.zshrc` 등의 파일에 환경변수 설정을 안해도 됨
  * `~/go` 디렉토리 생성
  * `~/go` 디렉토리 내에 `bin`, `pkg`, `src` 디렉토리 생성
  * 디렉토리 설정
```
  $ mkdir ~/go/src/github.com
  $ mkdir ~/go/src/github.com/{username}
  $ mkdir ~/go/src/github.com/{username}/gocode
  $ cd ~/go/src/github.com/{username}/gocode
  $ vi touch main.go
```

* VScode 실행 시 우측 하단에 go 관련 메시지가 표시되는데, 이 때 `Install All` 로 전부 설치


## AWS SDK for Go

* SDK 설치
  * `$ go get github.com/aws/aws-sdk-go`
    * `go.mod file not found...` 발생 시 `$ go env -w GO111MODULE=auto`

