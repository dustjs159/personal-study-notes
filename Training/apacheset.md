Apache Web Server Set
=================================
## Summary
- Last Updated : 21.06.12 Sat    
- Updated by : 윤연선
-----------------------------------

# Apache Setting

1. Apache 설치
   
```yum install httpd```
   
2. 방화벽 설정
   
<img width="577" alt="스크린샷 2021-06-08 오후 10 22 14" src="https://user-images.githubusercontent.com/57285121/121192503-fb87b280-c8a7-11eb-8e96-a0ebcf3e0840.png">
   
> * firewall-cmd 명령어를 통해 서비스 등록   

# Apache httpd 디렉토리 구조와 구성 요소
* /etc/httpd 확인
   
<img width="715" alt="스크린샷 2021-06-10 오후 4 05 33" src="https://user-images.githubusercontent.com/57285121/121480115-b24d7500-ca05-11eb-80b9-aa72f667e610.png">
   
## /etc/httpd/conf/httpd.conf
* Apache 웹서버 주 설정 파일

* ServerRoot
> * Apache 웹 서버의 root 디렉토리   
> * 웹 서버에 대한 설정, 로그 등이 위치할 서버의 디렉토리 위치 지정   

* Listen   
> * Apache 웹 서버의 포트 지정   

* Include   
> * 포함시켜 저장할 다른 설정 파일들을 적용   

* IfMoudle   
> * 특정 모듈이 존재하는 경우에만 작동하기 위한 설정   

* DocumentRoot   
> * 클라이언트에게 제공할 웹 페이지가 위치한 디렉토리 경로 지정   

* LoadModule   
> * /etc/httpd/modules의 모듈들을 읽어옴(so파일)   

* ServerAdmin   
> * 서버 오류시 클라이언트에게 전송할 오류 메시지에 들어갈 이메일 주소 설정   

* Directory : Apache에서 제공하는 웹 애플리케이션 디렉토리에 대한 설정('/'로 경로를 설정하면 모든 디렉토리에 적용)   
> * AllowOverride : .htaccess파일(인증을 담당) 사용 여부를 결정(All or None)   
> * Require : 해당 디렉토리의 접근 허용 여부 설정(denied or granted)   
> * Options : 지정한 디렉토리의 적용할 접근제어 설정
   
|옵션|설명|
|------|---|
|Indexes|클라이언트가 요청한 디렉토리 경로에 DirectoryIndex에서 설정한 파일이 없을 경우 디렉토리 목룍을 화면에 표시|
|FollowSymLinks|설정한 디렉토리에서 심볼릭 링크 허용|
   
* DirectoryIndex   
> * 클라이언트가 요청한 디렉토리에 대해 해당 파일을 반환할 파일 목록   

* Files   
> * 파일에 대한 옵션 설정(주로 접근권한)   

* ErrorLog   
> * 에러 로그가 생성될 경로 지정   

* LogLevel   
> * ErrorLog의 수준을 설정   

* LogFormat   
> * CustomLog의 형식을 지정   

* CustomLog   
> * Access 로그 파일이 저장되는 경로, 포맷을 설정   
> * LogFormat에서 지정한 형식을 불러와 사용 가능   

## /etc/httpd/conf.d
* Apache 웹서버 주 설정 파일에 포함된 하위 설정 파일
* autoindex.conf : 디렉토리의 내용을 로딩하는 방법에 대한 설정
* userdir.conf : 사용자 별 접근 웹 디렉토리에 대해 접근 권한을 설정
* welcome.conf
* README

## /etc/httpd/conf.modules.d
* 모듈들에 대한 conf파일 

## /etc/httpd/logs
* access_log : 웹 서버에 접근 시 발생하는 로그
* error_log : 에러 발생 시 발생하는 로그

## /etc/httpd/modules
* 설치되어 있는 모듈들


