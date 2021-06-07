Shell Script
====================================
## Summary
- Last Updated : 21.06.07 Mon   
- Updated by : 윤연선
-----------------------------------

# Shell
   
<img width="592" alt="스크린샷 2021-05-31 오전 1 34 34" src="https://user-images.githubusercontent.com/57285121/120112343-5c303480-c1b0-11eb-8d31-edf15a9edc12.png">
   
* 명령어 해석기
* 커널과 사용자 사이에서 사용자가 입력한 명령어를 해석하여 커널로 전달
* 커널의 처리 결과를 사용자에게 전달
* 주요 기능 및 역할   
> * 대화식 사용 : 사용자의 요청을 즉각 처리 및 결과를 출력하는 대화형 구조   
> * 프로그래밍 가능 : 복잡한 작업을 수행할 수 있도록 일련의 명령어들을 묶어서 사용 가능(Script)   
* /etc/shells 파일에 현재 사용할 수 있는 shell들의 경로가 설정되어 있음
   
<img width="414" alt="스크린샷 2021-05-31 오전 1 37 43" src="https://user-images.githubusercontent.com/57285121/120112441-cd6fe780-c1b0-11eb-89b0-cc6f48ca5d84.png">
   
## Shell의 종류
* sh(bourne shell)   
> * 유닉스의 가장 기본적인 shell   
> * 프로그래밍 언어를 사용하여 shell script구성 가능   

* bash(bourne again shell)   
> * **리눅스 표준 shell**   
> * sh 기반으로 만들어짐(sh와 호환됨)   
> * Alias(명령어 단축), History, 자동완성 등의 기능을 제공   

* csh(C shell)   
> * C언어 구문과 유사한 문법의 shell   

* ksh(korn shell)   
> * sh 기반으로 C shell을 추가하여 만든 shell

* zsh(z shell)   
> * sh 기반으로 만들어짐   
> * 실행 중인 shell끼리 명령어의 history 공유 가능   
> * 다양한 테마 지원   

* dash   
> * Ubuntu의 기본 shell   
> * Ubuntu에서는 가볍다는 장점때문에 일부 기능(history, 로그인 등)을 제외하고 기본 shell로 전환   

* tcsh(tc shell)   
> * csh 기반   
> * tcsh 스크립트 안에 함수를 정의할 수 없음   

## Shell 환경 변수
* 프로그램을 간편하게 실행시키기 위한 변수를 설정
* Shell에서 환경 변수 출력 명령어 : ```echo $환경변수```
* 로컬 환경 변수 값 등록 : ```set 환경변수=값```
* 전역 환경 변수 값 등록 : ```export 환경변수=값```   
> * 영구적으로 등록 : .bashrc(bash) / .zshrc(zsh)에 ```export 환경변수=값```   
* 환경 변수 값 삭제 : ```unset 환경변수```
* 환경 변수 목록 출력   
> * 로컬 환경 변수 : ```set```   
> * 전역 환경 변수 : ```printenv```   

* 주요 환경 변수
   
|환경변수|설명|
|------|---|
|HOME|현재 사용자의 홈 디렉토리|
|LANG|기본 지원되는 언어|
|TERM|로그인 터미널 타입|
|USER|현재 사용자 계정의 이름|
|BASH|bash shell 경로|
|ZSH|z shell 경로|
|HOSTNAME|호스트의 이름|
|PATH|실행 파일을 찾는 디렉토리 경로|
|PWD|사용자의 현재 작업 디렉토리|
|SHELL|로그인해서 사용하는 셸|
|OSTYPE|운영체제 타입|
   
# Shell Script
* 실행되어야 할 명령어의 순서, 방법을 정의한 Batch파일
* 자동화에서 많이 사용이 됨
* 프로그래밍 언어와 비슷하게 변수, 반복문, 제어문 사용 가능
* 프로그래밍 언어가 아니라 스크립트 언어이기 때문에 컴파일 과정이 필요 없음

## Shell Script 작성과 실행
* 스크립트 파일의 확장자는 스크립트 첫 줄의 선언문의 shell 이름을 사용(생략 가능)
* 스크립트 파일의 첫 줄에는 스크립트를 실행할 shell을 지정하는 선언문을 작성 :  ```#!사용할 shell디렉토리```
* 스크립트 파일의 실행은 ```선언문의shell이름 실행파일```

## Shell Script exit 
* Shell에서 프로그램을 종료하고 종료 상태에 대한 반환값(프로그래밍 언어의 return)을 얻기 위해 사용
* 스크립트가 성공적으로 수행되었는지 확인이 가능(Shell의 ```$?``` 를 통해 확인)
* ```exit [n]```   
* n=0 : 정상적으로 성공적인 종료 상태를 반환(True)   
* n=1 : 비정상적인 실패의 종료 상태를 반환(False)
   
<img width="616" alt="스크린샷 2021-05-27 오후 11 00 34" src="https://user-images.githubusercontent.com/57285121/119839725-597ad880-bf3f-11eb-83c3-d0d8329de4a1.png">
   
<img width="357" alt="스크린샷 2021-05-27 오후 11 06 41" src="https://user-images.githubusercontent.com/57285121/119840726-33a20380-bf40-11eb-8799-b88b134896db.png">
   
## Shell Script 문법 : 변수
* 변수는 변할 수 있는 값
* 상황에 따라 필요한 값을 계속 변경해 저장
* 별도의 변수 선언이 필요 없고 값 할당 시 자동으로 변수 생성
* 변수에 넣는 모든 값은 문자열 처리
* 대소문자 구별
* 변수 대입 시 '=' 좌우에는 공백없이 사용
* 변수들을 숫자로 변환하여 연산하고자 하는 경우에는 ``` `expr 수식` ``` 형태로 묶어줘야함

## Shell Script 문법 : 제어문(if & case)
* if ~ else
```
	if [ 조건 ]
	then
		True 일 때 실행
	else
		False일 때 실행
	fi
```
* 조건문에 들어가는 비교 연산자 
   
|비교 연산자|설명|
|------|---|
|-n "문자열"|문자열이 NULL이면 False|
|-z "문자열"|문자열이 NULL이면 True|
|수식1 -eq 수식2|두 수식을 비교하여 같으면 True ( '==' )|
|수식1 -ne 수식2|두 수식을 비교하여 같으면 False ( '!=' )|
|수식1 -gt 수식2|수식 1이 크면 True ( '>' )|
|수식1 -ge 수식2|수식 1이 크거나 같으면 True ( '>=' )|
|수식1 -lt 수식2|수식 1이 작으면 True ( '<' )|
|수식1 -le 수식2|수식 1이 작거나 같으면 True ( '<=' )| 
|!수식|수식의 NOT ( '!' )|
   
* 파일에 관련된 조건
   
|파일 조건|설명|
|------|---|
|-d 파일이름|파일이 디렉토리면 True|
|-e 파일이름|파일이 존재하면 True|
|-r 파일이름|파일이 읽기 가능이면 True|
|-w 파일이름|파일이 쓰기 가능이면 True|
|-x 파일이름|파일이 실행 가능이면 True|
   
* case ~ esac
```
	case $변수 in
		경우)
		명령;;
	exac
```
   
## Shell Script 문법 : 반복문(for & while)
* for ~ in
```
	for 변수 in 값1, 값2, 값3 ...
	do
		반복할 명령
	done
```


* while
```
	while [ 조건 ]
	do
		계속 반복할 명령
	done
		반복이 끝난 후 명령
```

