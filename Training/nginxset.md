Nginx Web Server Set
=================================
## Summary
- Last Updated : 21.07.01 Thu    
- Updated by : 윤연선
-----------------------------------

# Nginx Setting

1. ``yum install nginx``
   
# nginx 디렉토리 구조와 구성 요소
* /etc/nginx
   
<img width="608" alt="스크린샷 2021-06-12 오전 4 17 10" src="https://user-images.githubusercontent.com/57285121/121738345-102caa80-cb35-11eb-996d-9e203bf72643.png">
   
## /etc/nginx/nginx.conf
* Directive : nginx config 파일 구성 요소
* Directive는 Block 혹은 Contexts 단위의 그룹으로 구성
* Directive는 괄호 블록('{ }')이나 세미콜론(';')으로 끝나야함
* 웹 서버의 기본적인 동작을 정의하는 core directive
   
<img width="335" alt="스크린샷 2021-06-12 오전 4 37 47" src="https://user-images.githubusercontent.com/57285121/121740357-f2147980-cb37-11eb-9b53-94ab20dce976.png">
   
> * user : nginx 사용자. nginx 웹 서버를 동작시키는 사용자 기술   
> * worker_processes : worker process의 개수를 지정   
> * error_log : 에러 로그가 기록될 파일의 경로를 설정   
> * pid : nginx PID가 기록된 파일   
* events 블록
      
<img width="284" alt="스크린샷 2021-06-12 오후 2 21 18" src="https://user-images.githubusercontent.com/57285121/121765947-77744a00-cb89-11eb-8655-531cbffd3930.png">
   
> * worker_connections : worker process 하나당 처리할 connection의 수   
* http 블록
   
<img width="700" alt="스크린샷 2021-06-13 오전 12 08 32" src="https://user-images.githubusercontent.com/57285121/121780484-7f5cda00-cbdb-11eb-92e0-561d7ba7e9c1.png">
   
> * 서버의 기본값들을 설정   
> * http 블록의 설정들은 server 블록과 location 블록에도 적용됨   
* server 블록
   
<img width="578" alt="스크린샷 2021-06-13 오전 12 42 15" src="https://user-images.githubusercontent.com/57285121/121781534-35c2be00-cbe0-11eb-90e0-3bac1576e071.png">
   
> * 하나의 웹 사이트를 선언하는데 사용   
> * 여러 server 블록으로 하나의 호스트에서 여러 서버를 운영할 수 있음**(가상호스트)**   
* location 블록
   
<img width="373" alt="스크린샷 2021-06-13 오전 12 43 35" src="https://user-images.githubusercontent.com/57285121/121781583-6571c600-cbe0-11eb-9027-6b4ee922f407.png">
   
> * 웹사이트의 URI를 처리하는데 사용


## Nginx 수동 설치하기

1. nginx 홈페이지에서 wget 명령어로 사용 가능한 최신 버전 압축파일 다운로드(Stable version)   
> * 설치 링크 : http://nginx.org/en/download.html   
> * 설치 명령어 : ``$ wget http://nginx.org/download/nginx-1.20.1.tar.gz``   
   
<img width="767" alt="스크린샷 2021-06-30 오후 5 35 33" src="https://user-images.githubusercontent.com/57285121/123929243-9e27e280-d9c9-11eb-913f-bc8431e3c0f0.png">
   
2. 추가 라이브러리 설치
* nginx를 컴파일 설치하기 위해서는 몇 가지의 라이브러리 추가 설치가 필요함
* openSSL
* PCRE
* zlib

2-1. openSSL 설치
* openSSL : SSL 오픈소스 라이브러리화   
> * 설치 링크 : https://www.openssl.org/source/
> * 설치 명령어 : ``$ wget https://www.openssl.org/source/openssl-3.0.0-beta1.tar.gz``   

2-2. PCRE 설치
* pcre2는 컴파일 에러가 뜨기 때문에 pcre를 사용
* 최신 버전의 pcre 다운로드(나는 8.45)   
> * 설치 링크 : https://sourceforge.net/projects/pcre/files/pcre/   
> * 설치 명령어 : ``$ wget https://sourceforge.net/projects/pcre/files/pcre/8.45/pcre-8.45.tar.gz``

2-3. zlib 설치
* zlib : 데이터 압축 라이브러리   
> * 설치 링크 : https://zlib.net/fossils/   
> * 설치 명령어 : ``$ wget https://zlib.net/fossils/zlib-1.2.11.tar.gz``

3. 압축 해제
* 확장자가 .tar.gz로 되어있는 압축파일들을 해제      
* nginx 압축 파일을 먼저 해제한 후 그 해당 디렉토리 내에 openssl, pcre, zlib 순서로 압축 해제
> * 압축 해제 명령어 : ``$ tar -xvf <압축파일>``
   
<img width="581" alt="스크린샷 2021-06-30 오후 8 53 31" src="https://user-images.githubusercontent.com/57285121/123956034-3b444480-d9e5-11eb-926b-a27ce6db7a9e.png">
   
<img width="565" alt="스크린샷 2021-06-30 오후 9 49 46" src="https://user-images.githubusercontent.com/57285121/123963109-181d9300-d9ed-11eb-8472-37105dffdb08.png">
   
4. 소스 패키지 설치
* 소스 패키지 설치는 confiugre / make / make install 세 단계로 진행

4-0. c언어 컴파일러 gcc패키지 설치
* c언어로 짜여진 소스 코드를 컴파일 하기위한 gcc 패키지 설치   
> * ``$ yum install gcc*``   

4-1. configure
* 경로 설정 및 같이 빌드할 라이브러리들을 지정하고 결과물로 makefile을 생성   
> * ``$ ./configure --prefix=/home/yys/apps/nginx --with-zlib=./zlib-1.2.11 --with-pcre=./pcre-8.45 --with-openssl=./openssl-3.0.0-betal``

4-2. make
* 소스 코드 컴파일   
> * ``$ make``

4-3. make install
* 설치   
> * ``$ make install``   

5. 서비스 유닛 수동 등록
* 이렇게 설치까지는 완료되었으나 서비스 등록이 되어있지 않아 관리가 어렵다.
* 서비스 유닛을 수동으로 등록해줘야 함
* /usr/lib/systemd/system에 nginx.service 파일 생성
* nginx 서비스 유닛에 다음과 같은 항목 작성
   
 <img width="477" alt="스크린샷 2021-07-01 오후 11 11 04" src="https://user-images.githubusercontent.com/57285121/124138445-9d727780-dac1-11eb-80aa-39d9bdaa7182.png">
  
5-1. 서비스 유닛 수동 등록을 위한 Nginx 명령어
* ``$ nginx`` : nginx 시작
* ``$ nginx -s stop`` : nginx 정지
* ``$ nginx -s reload`` : nginx 리로드
* ``$ nginx -t`` : nginx 설정파일 체크
* ``$ nginx -v`` : nginx 버전 확인

6. 테스트
* ``$ systemctl start nginx``
* 만약 시작이 되지 않는다면 ``$ journalctl -xe``로 오류 내용 확인
* Selinux 관련 문제가 생겼다면 /etc/sysconfig/selinux/selinux 파일을 열어 SELINUX=disabled로 변경
   
<img width="765" alt="스크린샷 2021-07-01 오후 5 52 01" src="https://user-images.githubusercontent.com/57285121/124095872-0abbe380-da95-11eb-8eac-d91dd7c27dbe.png">
   
* 저장 후 네트워크 재시작 : ``$ systemctl restart NetwokrManager``

* firewalld에 http 서비스 등록 : ``$ firewall-cmd --permanent --add-service=http``
* firewalld 변경 사항 리로드 : ``$ firewall-cmd --reload``
* IP 주소로 접속하면 페이지에 '403 Forbidden' 발생
* ~/nginx/logs의 'error.log' 파일 확인
   
<img width="755" alt="스크린샷 2021-07-01 오후 6 54 27" src="https://user-images.githubusercontent.com/57285121/124105009-c54fe400-da9d-11eb-9cd4-0987857f76a3.png">
   
* 권한 관련 문제
* ~/nginx/conf/nginx.conf 파일의 'user' 지시자를 내 계정으로 변경
   
<img width="98" alt="스크린샷 2021-07-01 오후 6 56 32" src="https://user-images.githubusercontent.com/57285121/124105302-0ea03380-da9e-11eb-9f94-a20a595b61b9.png">
   
* nginx 리로드 : ``$ systemctl reload nginx``
* 웹에서 접속
   
<img width="404" alt="스크린샷 2021-07-01 오후 6 57 33" src="https://user-images.githubusercontent.com/57285121/124105476-342d3d00-da9e-11eb-95b3-0de257dd4611.png">
   
* 접속 성공

## 포트 번호 변경
* nginx 웹 서버의 포트 번호를 18080으로 변경
* ~/nginx/conf/nginx.conf의 http 블록 내 server 블록에 'listen'을 18080로 변경
   
<img width="268" alt="스크린샷 2021-07-01 오후 11 14 06" src="https://user-images.githubusercontent.com/57285121/124138868-0a860d00-dac2-11eb-9b27-fe25d2b9414f.png">
   
* 포트번호 허용(영구적)
* ``$ firewall-cmd --permanent --add-port=18080/tcp``
   
<img width="442" alt="스크린샷 2021-07-01 오후 11 15 26" src="https://user-images.githubusercontent.com/57285121/124139138-4c16b800-dac2-11eb-97bf-7595ede7b855.png">
   
* 포트번호 18080으로 접속
   
<img width="403" alt="스크린샷 2021-07-01 오후 11 16 23" src="https://user-images.githubusercontent.com/57285121/124139213-5c2e9780-dac2-11eb-81a2-cb97fe76f92d.png">
   
## 로그 경로 변경
* access_log와 error_log 경로 변경
* ~/nginx/conf/nginx.conf의 http 블록 내에 access_log와 error_log의 경로를 변경
   
<img width="537" alt="스크린샷 2021-07-02 오전 12 47 20" src="https://user-images.githubusercontent.com/57285121/124153131-11674c80-dacf-11eb-9df2-63eead1e39be.png">
   
* nginx 재시작 후 확인 : ``$ systemctl reload nginx``
   
<img width="766" alt="스크린샷 2021-07-02 오전 12 48 44" src="https://user-images.githubusercontent.com/57285121/124153324-4378ae80-dacf-11eb-8232-d28e58a41d7c.png">
   
* 로그 경로 변경

## 도메인으로 접속

 





