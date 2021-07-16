Apache Install & Set
=================================
## Summary
- Last Updated : 21.07.16 Fri    
- Updated by : 윤연선
-----------------------------------
## Apache 설치과정과 구성환경 및 실습 테스트
* 본 글은 CentOS 8 환경에서 작성했습니다. 
---------------------------------

## 1. Apache 패키지 설치

* yum을 사용하여 Apache 패키지 설치   
> * ``$ yum install httpd``

## 2. Apache 수동 설치하기
* ``$ cd /usr/local/src``

1. Apache 홈페이지에서 wget 명령어로 사용 가능한 최신 버전 압축파일 다운로드(Stable Release)   
> * 설치 링크 :  http://httpd.apache.org/download.cgi  
> * 설치 명령어 : ``$ wget https://mirror.navercorp.com/apache//httpd/httpd-2.4.48.tar.gz``   
   
<img width="727" alt="스크린샷 2021-07-07 오전 1 35 17" src="https://user-images.githubusercontent.com/57285121/124636540-9ed9e080-dec3-11eb-82ee-35868e6fb67d.png">
   
2. 추가 라이브러리 설치
* Apache를 컴파일 설치하기 위해서는 몇 가지의 라이브러리 추가 설치가 필요함
* apr
* apr-util
* pcre

2-1. apr 설치
* APR(Apache Portable Runtime) : apache 웹 서버 지원 라이브러리    
> * 설치 링크 : http://mirror.apache-kr.org/apr/   
> * 설치 명령어 : ``$ wget http://mirror.apache-kr.org/apr/apr-1.7.0.tar.gz``   

2-2. apr-util 설치
* apr과 함께 설치
> * 설치 링크 : http://mirror.apache-kr.org/apr/   
> * 설치 명령어 : ``$ wget http://mirror.apache-kr.org/apr/apr-util-1.6.1.tar.gz``

2-3. pcre 설치
* pcre2는 컴파일 에러가 뜨기 때문에 pcre를 사용   
> * 설치 링크 : https://ftp.pcre.org/pub/pcre/
> * 설치 명령어 : ``$ wget https://ftp.pcre.org/pub/pcre/pcre-8.45.tar.gz``
   
<img width="614" alt="스크린샷 2021-07-07 오전 1 37 28" src="https://user-images.githubusercontent.com/57285121/124636794-e5c7d600-dec3-11eb-8e7f-8ac9152bad16.png">
   
3. 압축 해제
* 확장자가 .tar.gz로 되어있는 압축파일들을 해제      
* httpd 압축 파일을 먼저 해제한 후 그 해당 디렉토리 내에 apr, apr-util, pcre 순서로 압축 해제
> * 압축 해제 명령어 : ``$ tar -xvf <압축파일>``
   
3-1. 압축해제 후 압축 파일들은 삭제
* ``$ rm <압축파일>``
   
<img width="523" alt="스크린샷 2021-07-07 오전 1 48 59" src="https://user-images.githubusercontent.com/57285121/124638091-823ea800-dec5-11eb-8d02-275df60d9b8c.png">
   
4. 소스 패키지 설치
* 소스 패키지 설치는 confiugre / make / make install 세 단계로 진행

4-0. c언어 컴파일러 gcc패키지 설치
* c언어로 짜여진 소스 코드를 컴파일 하기위한 gcc 패키지 설치   
> * ``$ yum install gcc*``   
   
4-1. pcre 설치   
> * ``$ cd /usr/local/src/pcre``   
> * ``$ yum install pcre-devel``   
> * ``$ ./configure --prefix=/usr/local/src/pcre``   
> * ``$ make``   
> * ``$ make install``  

4-2. apr 설치
> * ``$ cd /usr/local/src/apr-1.7.0``   
> * ``$ ./configure --prefix=/usr/local/src/httpd-2.4.48/srclib/apr``   
> * cannot remove 'libtoolT' 발생 시 ``$ cp -arp libtool libtoolT``   
> * ``$ make``   
> * ``$ make install``   

4-3. apr-util 설치   
> * ``$ cd /usr/local/src/apr-util-1.6.1``   
> * ``$ ./configure --prefix=./configure --prefix=/usr/local/src/httpd-2.4.48/srclib/apr-util --with-apr=/usr/local/src/httpd-2.4.48/srclib/apr``   
> * ``$ make``   
> * 여기서 'expat.h no such file or directory' 오류 발생 시 'expat-devel' 설치 : ``$ yum install expat-devel``   
> * ``$ make install``   

4-4. apache httpd 설치   
> * ``$ cd /usr/local/src/httpd-2.4.48``   
> * ``$ ./configure --prefix=/usr/local/apache --with-apr=/usr/local/src/httpd-2.4.48/srclib/apr --with-apr-util=/usr/local/src/httpd-2.4.48/srclib/apr-util --with-pcre=/usr/local/src/pcre``   
> * ``$ make``   
> * ``$ make install``   
   
<img width="487" alt="스크린샷 2021-07-07 오전 3 19 45" src="https://user-images.githubusercontent.com/57285121/124648408-2fb7b880-ded2-11eb-82f1-d401b343f448.png">
     
5. 테스트

5-1. ServerName 및 Listen 설정
* /usr/local/apache/conf/httpd.conf의 ServerName, Listen 지시자의 주석을 해제
   
<img width="219" alt="스크린샷 2021-07-07 오후 2 09 31" src="https://user-images.githubusercontent.com/57285121/124703280-fa8c8400-df2c-11eb-866e-9f53cb9a1b16.png">
   
<img width="152" alt="스크린샷 2021-07-07 오후 2 20 20" src="https://user-images.githubusercontent.com/57285121/124704105-789d5a80-df2e-11eb-9b73-664facf5cdda.png">
   
5-2. apachectl 명령어
* 경로는 /usr/local/apache/bin      
> * ``$ ./apachectl start`` : httpd 시작   
> * ``$ ./apachectl stop`` : httpd 정지   
> * ``$ ./apachectl status`` : httpd 상태 확인   
> * ``$ ./apachectl graceful`` : httpd reload   
> * ``$ ./apachectl restart`` : httpd 재시작   
> * ``$ ./apachectl configtest`` : httpd 설정파일 체크   
> * ``$ ./apachectl -v`` : httpd 버전 확인   

5-3. httpd 시작 및 포트확인   
* ``$ ./apachectl start``
* ``$ netstat -nlpt``
   
<img width="871" alt="스크린샷 2021-07-07 오후 2 15 28" src="https://user-images.githubusercontent.com/57285121/124703879-13e20000-df2e-11eb-9969-41b99e70eadb.png">
   
> * 80번 포트 Listen(대기중)   

5-4. 80번 포트 방화벽 허용
* 영구적으로 tcp를 사용하는 80번 포트에 접근 허용   
> * ``$ firewall-cmd --permanent --zone=public --add-port=80/tcp``   

* firewalld 리로드   
> * ``$ firewall-cmd --reload``
   
<img width="707" alt="스크린샷 2021-07-07 오후 2 24 17" src="https://user-images.githubusercontent.com/57285121/124704430-05e0af00-df2f-11eb-9c4a-cc85a568dfe1.png">
   
5-5. 웹에서 접속
   
<img width="316" alt="스크린샷 2021-07-07 오후 2 27 31" src="https://user-images.githubusercontent.com/57285121/124704709-78518f00-df2f-11eb-841d-de97e453d92a.png">
   
## Apache httpd 디렉토리 구조와 구성 요소
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

# Apache 실습 테스트
## 포트 번호 변경 (port : 18080)

1. firewall-cmd 명령어로 허용할 port 추가   
> * ``$ firewall-cmd --permanent --zone=public --add-port=18080/tcp``   
> * reload : ``$ firewall-cmd --reload``   
   
<img width="481" alt="스크린샷 2021-06-26 오전 12 06 22" src="https://user-images.githubusercontent.com/57285121/123444886-580e0000-d612-11eb-91b0-c23d0b63048e.png">

2. ~/conf/httpd.conf 파일의 Listen 지시자에 18080 추가
   
<img width="137" alt="스크린샷 2021-06-26 오전 12 11 08" src="https://user-images.githubusercontent.com/57285121/123445605-03b75000-d613-11eb-9244-9e696bfdfb67.png">
   
3. 결과 확인
   
<img width="362" alt="스크린샷 2021-06-26 오전 12 11 40" src="https://user-images.githubusercontent.com/57285121/123445673-16318980-d613-11eb-911f-1091b3dd60fb.png">
   
## access / error log 경로 변경
1. 로그를 생성할 별도의 디렉토리 생성
* 경로는 /usr/local/apache/mylogs      
> * ``$ mkdir mylogs``   

2. ~conf/httpd.conf의 CustomLog 지시자의 경로 변경
   
<img width="416" alt="스크린샷 2021-07-09 오후 11 50 38" src="https://user-images.githubusercontent.com/57285121/125096835-77c41e80-e110-11eb-818f-51117d3a0c66.png">
   
<img width="300" alt="스크린샷 2021-07-09 오후 11 49 52" src="https://user-images.githubusercontent.com/57285121/125096708-5e22d700-e110-11eb-88a9-8f7bd53a207c.png">
   
3. 로그 확인
   
<img width="758" alt="스크린샷 2021-07-09 오후 11 57 02" src="https://user-images.githubusercontent.com/57285121/125097707-5d3e7500-e111-11eb-9c74-0b129438ce17.png">
   
## 도메인으로 접속하기
* 리눅스 호스트 파일
* /etc/hosts
* DNS보다 먼저 참조하게 하여 외부로 오픈 전 미리 **로컬에서만** 테스트 용도로 사용
* DNS에 등록되지 않은 사이트를 이용할 때 사용. 대신 로컬에서만.
* CentOS의 hosts 기본설정
   
<img width="709" alt="스크린샷 2021-07-10 오전 2 07 04" src="https://user-images.githubusercontent.com/57285121/125113358-87009780-e123-11eb-8805-262f3ad8f1f6.png">
   
> * 좌측부터 IP, 호스트명(도메인명), Alias 순서   

1. 매핑할 IP와 도메인을 설정
   
<img width="374" alt="스크린샷 2021-07-16 오후 3 43 25" src="https://user-images.githubusercontent.com/57285121/125903957-3bd1a239-d93c-40b1-800a-239ee03699b4.png">
   
> * 'yysdomain.com' URL로 접속하면 현재 IP인 172.16.123.13로 접속되도록 설정, Alias는 'yys'로 설정   

2. 네트워크 재시작   
> * ``$ systemctl restart NetworkManager``   

3. 로컬에서 호스트명과 Alias로 접속
   
<img width="382" alt="스크린샷 2021-07-10 오전 2 46 07" src="https://user-images.githubusercontent.com/57285121/125117290-fb8a0500-e128-11eb-9b3b-6f483f2695e4.png">
   
<img width="307" alt="스크린샷 2021-07-16 오후 3 50 07" src="https://user-images.githubusercontent.com/57285121/125904706-c7300eea-8966-4596-935c-adce44b3bef5.png">
   
4. hosts 파일의 변경사항을 확인   
   
<img width="690" alt="스크린샷 2021-07-16 오후 4 00 34" src="https://user-images.githubusercontent.com/57285121/125905963-04bd9a68-c847-4416-8e98-080bb615a1a5.png">
   
> * ``$ ping 호스트명``
   
<img width="689" alt="스크린샷 2021-07-16 오후 4 01 25" src="https://user-images.githubusercontent.com/57285121/125906055-a9d8efff-d8ce-4ac7-b07f-d23b1ea59ccd.png">
   
> * ``$ ping 호스트 Alias``   
> * Alias로 ping을 테스트 해도 호스트명으로 인식   

## 가상 호스트 설정하기
* 가상 호스트를 구성하여 default 호스트 뿐만 아니라 가상의 호스트들을 구성하여 여러 웹페이지를 출력
* httpd-vhosts.conf 파일의 기본설정
   
<img width="590" alt="스크린샷 2021-07-16 오후 4 36 08" src="https://user-images.githubusercontent.com/57285121/125910299-ee6212ff-e9a1-460e-a447-c98ab36d04bb.png">
   
1. /etc/hosts 파일에서 IP 주소와 호스트명(도메인명), Alias를 지정
   
<img width="373" alt="스크린샷 2021-07-16 오후 4 39 21" src="https://user-images.githubusercontent.com/57285121/125910705-bc9ff7d8-9d19-4253-8d7f-372f44cfde5a.png">
   
2. hosts 파일 변경사항 반영을 위한 NetworkManager 데몬 재시작   
> * ``$ systemctl restart NetworkManager``

3. httpd-vhosts.conf 파일의 VirtualHost 지시자 설정 변경
   
<img width="479" alt="스크린샷 2021-07-16 오후 5 13 43" src="https://user-images.githubusercontent.com/57285121/125915424-45113cc7-5180-41a7-bb9b-c61e74454897.png">
   
> * DocumentRoot, ErrorLog/CustomLog, DirectoryIndex는 개별 생성   

4. ~/docs 의 vhost1.html, vhost2.html 내용(출력할 웹 페이지) 입력
```html
<html>
<body>
<h1> This is Web Page is Vhost1 </h1>
</body>
</html>
```
> * 두 개 생성. 하나는 Vhost2   

5. 변경사항 반영
* 가상호스트 httpd.conf 파일에 Include conf/extra/httpd-vhosts.conf 추가
   
<img width="342" alt="스크린샷 2021-07-16 오후 5 24 22" src="https://user-images.githubusercontent.com/57285121/125916889-b7192f36-7f50-4813-9034-6ccef6ed8ec9.png">
    
6. 접근 권한 설정
* conf/httpd.conf파일에 다음과 같이 추가
   
<img width="325" alt="스크린샷 2021-07-16 오후 5 41 13" src="https://user-images.githubusercontent.com/57285121/125919321-ac8031e1-0b72-4f91-bb47-5b18c9a272d7.png">
   
6. 재시작과 테스트   
> * ``$ ./apachectl graceful``   

<img width="463" alt="스크린샷 2021-07-16 오후 5 43 39" src="https://user-images.githubusercontent.com/57285121/125919670-3658cbd6-3a0c-4c66-bb9d-596d94baa2e6.png">
   
<img width="489" alt="스크린샷 2021-07-16 오후 5 43 57" src="https://user-images.githubusercontent.com/57285121/125919719-1e56fac7-f3f0-49d0-b9e9-9fd5ba160289.png">
   

