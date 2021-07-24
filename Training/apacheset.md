Apache Install & Set
=================================
## Summary
- Last Updated : 21.07.23 Fri    
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
   
## httpd 제어 command : apachectl vs httpd
* 아파치의 웹 서버 데몬 이름은 httpd
* 이 httpd를 제어하는 명령어는 두 가지가 존재
* apachectl은 ~/apache/bin에 스크립트 파일로 존재하고 httpd는 바이너리 파일로 존재
* 

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

## 가상 호스트(Virtual Host) 설정하기
* 가상 호스트는 서버에 IP / 도메인 / 포트번호로 접속할 때 각각 다른 웹 사이트를 띄우기 위한 기술
* 가상 호스트의 구성 방법   
> * 이름 기반(가장 자주 사용되는 방법)   
> * 포트 기반   
> * IP 기반   
> * 이름- IP 혼합   

* 이름 기반 가상 호스트   
> * 서버는 하나의 IP 주소에 대해 여러 호스트 이름을 갖고 클라이언트 요청의 Hosts 헤더에 따라 여러 웹 페이지를 호스팅   
 
1. /etc/hosts 파일 수정
* 호스팅할 서버의 IP 주소와 여러 호스트 이름을 매핑
   
<img width="384" alt="스크린샷 2021-07-19 오후 6 32 58" src="https://user-images.githubusercontent.com/57285121/126138500-b8e98181-fb81-486d-a5ab-d0b3777f9958.png">
   
* 수정 후 네트워크 재시작   
> * ``$ systemctl restart NetworkManager``

2. ~/conf/extra/httpd-vhosts.conf 파일 설정
   
<img width="502" alt="스크린샷 2021-07-19 오후 6 42 06" src="https://user-images.githubusercontent.com/57285121/126139962-a5df223f-af93-4c6a-a305-eaeaff8452f1.png">
   
> * 여기서 'mydocs', 'mylogs' 디렉토리와 'view.html' 파일은 은 경로에 맞게 생성   

3. ~/mydocs 의 view.html 내용(출력할 웹 페이지) 입력
```html
<html>
<body>
<h1>It Virtual Host works!</h1>
</body>
</html>
```
5. 변경사항 반영
* ~/conf/httpd.conf 파일에 #Include conf/extra/httpd-vhosts.conf 주석 해제 또는 추가
   
<img width="342" alt="스크린샷 2021-07-16 오후 5 24 22" src="https://user-images.githubusercontent.com/57285121/125916889-b7192f36-7f50-4813-9034-6ccef6ed8ec9.png">
   
6. 재시작과 테스트   
> * ``$ ./apachectl graceful``
   
<img width="486" alt="스크린샷 2021-07-19 오후 6 54 14" src="https://user-images.githubusercontent.com/57285121/126141903-43431a2c-ef5a-485f-8384-9d9d968a53e6.png">  
   
<img width="430" alt="스크린샷 2021-07-19 오후 6 54 46" src="https://user-images.githubusercontent.com/57285121/126141975-a84db732-c0ce-4fbe-8a46-cd36d41b4045.png">
   
<img width="592" alt="스크린샷 2021-07-19 오후 6 56 31" src="https://user-images.githubusercontent.com/57285121/126142244-9b2aee58-a8bf-467d-a0fc-63a480652c29.png">
   
## httpd 서비스 수동 등록
* 아파치 컴파일 설치시 httpd 데몬이 systemd에 등록되어있지 않습니다.
* httpd 데몬을 수동으로 등록하는 과정입니다.

1. 파일 생성   
> * ``$ vi /usr/lib/systemd/system/httpd.service``

2. 유닛 구성 항목 작성
   
<img width="462" alt="스크린샷 2021-07-23 오후 5 32 44" src="https://user-images.githubusercontent.com/57285121/126756808-448a05b4-ebf7-4b60-bb0b-5d01f4c0c731.png">
   
3. systemd 데몬 재시작 및 httpd 데몬 실행   
> * ``$ systemctl daemon-reload``   
> * ``$ systemctl start httpd``   

4. 상태 점검 및 테스트   
> * ``$ systemctl status httpd``   
   
<img width="668" alt="스크린샷 2021-07-23 오후 5 36 06" src="https://user-images.githubusercontent.com/57285121/126757140-57d06930-7bcc-4801-b55a-5f16eb9417ab.png">
   
<img width="342" alt="스크린샷 2021-07-23 오후 5 36 28" src="https://user-images.githubusercontent.com/57285121/126757178-1abe9d0e-6021-4c7a-8a8c-844fd3c1d8fa.png">
   
## Logrotate
* 서버를 운영함에 있어서 로그를 관리하는 것은 중요합니다.
* 로그를 확인하여 외부로 부터의 공격을 방어할 수 있고 시스템 장애를 예방할 수 있습니다.
* 하지만 로그가 관리되지 않고 지속적으로 쌓여갈 경우 로그 확인이 어려워질 뿐더러 로그 저장공간의 낭비가 발생할 수 있습니다.
* Logrotate는 이러한 로그를 관리할 수 있는 도구입니다.
* 설정에 따라 오래되거나 일정 개수 이상의 로그가 보관되면 삭제하거나 등의 로그가 저장된 디렉토리를 정리(rotate)
* /etc/logrotate.conf : logrotate의 설정
* /etc/logrotate.d/~ : logrotate를 설정할 데몬들
* logrotate 설치   
> * ``$ yum install loglotate``   
* /etc/logrotate.conf 파일의 기본구성
  
<img width="594" alt="스크린샷 2021-07-23 오후 9 49 08" src="https://user-images.githubusercontent.com/57285121/126783821-82307442-b010-4814-9aa7-d0c23e6c8312.png">
   
> * weekly : 로그 백업 주기. daily(매일), weekly(매주), monthly(매월), yearly(매년)의 주기를 설정할 수 있음   
> * rotate 4 : 저장할 로그의 기간. 로그 백업 주기에 따라 설정 가능함. Ex) 로그 백업 주기가 daily에 rotate 5라고 한다면 최대 5일치의 로그만 저장하고 6 일째부터는 1 일차 로그부터 순차적으로 삭제되면서 저장됨   
> * create : 로그 파일 정리 후 계속해서 새로운 파일을 생성할지 안할지 여부 선택   
> * dateext : 로그 파일을 저장할 때 파일명에 날짜를 부여하여 저장함   
> * compress : 로그 파일을 압축하여 저장(크기를 줄여서 저장하기 때문에 저장공간을 효율적으로 사용가능)   
> * include ~ : logrotate를 적용할 데몬 설정   
> * missingok : 로그파일이 없더라도 에러처리 안하고 넘어감   
> * notifempty : 로그 파일이 비어있으면 rotate 안함   
> * postrotate(or prerotate) ~ endscript : rotate 후 실행할 작업 설정   
> * sharedscripts : postrotate (or prerotate) ~ endscript의 작업을 한번만 수행

1. /etc/logrotate.d/httpd 파일을 수정
   
<img width="391" alt="스크린샷 2021-07-24 오전 1 07 12" src="https://user-images.githubusercontent.com/57285121/126810409-60f3e285-f2dd-4463-8ec5-d6fd86042f88.png">   
   
2. httpd 실행   
> * ``$ systemctl start httpd``   

3. rotate 실행   
> * 강제 실행 : ``$ /usr/sbin/logrotate -f /etc/logrotate.d/httpd``   
> * 디버그 : ``$ /usr/sbin/logrotate -d /etc/logrotate.d/httpd``   
> * 실행 이력 확인 : ``$ /usr/sbin/logrotate -v /etc/logrotate.d/httpd``
   
<img width="570" alt="스크린샷 2021-07-24 오전 1 12 52" src="https://user-images.githubusercontent.com/57285121/126811067-12e18955-7e23-4465-8d20-9e5218e75596.png">
   
<img width="672" alt="스크린샷 2021-07-24 오전 1 16 38" src="https://user-images.githubusercontent.com/57285121/126811528-3065cfd3-3b02-4103-b7af-dbefb47a0c65.png">
   
## log level
* 에러 로그를 기록하는데에 있어서 위험한 정도에 따라 로그 레벨이 다름
* LogLevel에 설정한 로그 레벨 미만의 위험도의 에러는 로그에 기록하지 않음
* httpd.conf의 LogLevel 지시자로 변경 가능
   
|LogLevel|의미|
|------|---|
|emerg|서버 작동이 안될 수준의 심각한 오류|
|alert|crit보다 심각한 오류|
|crit|치명적 오류|
|error|오류|
|warn|경고|
|notice|알림메시지|
|info|서버 정보|
|debug|디버깅을 위한 정보|
   
* 별도의 index.html파일을 만들지 않고 에러 로그 출력해보기
1. httpd.conf 의 LogLevel을 emerge로 설정 후 테스트   
> * ``$ tail -f error_log``   
   
<img width="1416" alt="스크린샷 2021-07-24 오전 1 31 53" src="https://user-images.githubusercontent.com/57285121/126813278-77b84e85-4486-474c-9e9d-78109777d982.png">
   
> * 아무 로그도 출력되지 않음.

2. httpd.conf 의 LogLevel을 warn으로 설정 후 테스트   
> * 변경 후 ``$ systmectl reload httpd``   
> * ``$ tail -f error_log``   

<img width="753" alt="스크린샷 2021-07-24 오전 1 36 03" src="https://user-images.githubusercontent.com/57285121/126813708-711972e7-05fa-4eab-8bcc-a2f847a84827.png">
   
> * 치명적이진 않지만 경고 수준의 에러 로그 확인 가능

## 인증서 발급(Let's encrypt)
* 웹 사이트의 신뢰성을 보장하기 위한 인증서를 발급받아 웹 서버에 적용하기
* Let's encrypt 인증서를 무료로 발급받아 아파치 웹서버에 적용
* 무료라는 장점이 있지만 3 개월마다 갱신을 해줘야 하는 단점이 존재
* Let's encrypt를 통해 인증서를 발급받기 전 Certbot을 먼저 설치해야함
* 인증서를 발급하기 위해서는 먼저 무료로 도메인을 하나 발급받아야 함   
> * 무료 인증서 발급(freenom) : www.freenom.com   

1. Certbot 설치   
> * EPEL 저장소 설치 : ``$ yum install epel-release``   
> * ``$ yum install certbot``   
> * ``$ yum install certbot python3-certbot-apache mod_ssl``   

2. 인증서 받기   
> * ``$ certbot certonly -d <도메인명>``   
   
<img width="753" alt="스크린샷 2021-07-24 오전 2 37 16" src="https://user-images.githubusercontent.com/57285121/126820657-70562251-8b44-4d19-9774-258dcf19090a.png">
   
 
