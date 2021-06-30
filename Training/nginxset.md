Nginx Web Server Set
=================================
## Summary
- Last Updated : 21.06.30 Wed    
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
   
> * user : nginx 사용자   
> * worker_processes : worker process의 개수를 지정   
> * error_log : 에러 로그가 기록될 파일의 경로를 설정   
> * pid : process ID가 기록될 파일   
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
> * 설치 링크 : [nginx]http://nginx.org/en/download.html   
> * 설치 명령어 : ``wget http://nginx.org/download/nginx-1.20.1.tar.gz``   
   
<img width="767" alt="스크린샷 2021-06-30 오후 5 35 33" src="https://user-images.githubusercontent.com/57285121/123929243-9e27e280-d9c9-11eb-913f-bc8431e3c0f0.png">
   
2. 추가 라이브러리 설치
* nginx를 컴파일 설치하기 위해서는 몇 가지의 라이브러리 추가 설치가 필요함
* openSSL
* PCRE
* zlib

2-1. openSSL 설치
* openSSL : SSL 오픈소스 라이브러리화   
> * 설치 링크 : [openssl]https://www.openssl.org/source/
> * 설치 명령어 : ``wget https://www.openssl.org/source/openssl-3.0.0-beta1.tar.gz``   

2-2. PCRE 설치
* pcre2는 컴파일 에러가 뜨기 때문에 pcre를 사용
* 최신 버전의 pcre 다운로드(나는 8.45)   
> * 설치 링크 : [pcre]https://sourceforge.net/projects/pcre/files/pcre/   
> * 설치 명령어 : ``wget https://sourceforge.net/projects/pcre/files/pcre/8.45/pcre-8.45.tar.gz``

2-3 zlib 설치
* zlib : 데이터 압축 라이브러리   
> * 설치 링크 : [zlib]https://zlib.net/fossils/   
> * 설치 명령어 : ``wget https://zlib.net/fossils/zlib-1.2.11.tar.gz``

3. 압축 해제
* 확장자가 .tar.gz로 되어있는 압축파일들을 해제      
* nginx 압축 파일을 먼저 해제한 후 그 해당 디렉토리 내에 openssl, pcre, zlib 순서로 압축 해제
> * 압축 해제 명령어 : ``tar -xvf <압축파일>``
   
<img width="565" alt="스크린샷 2021-06-30 오후 9 49 46" src="https://user-images.githubusercontent.com/57285121/123963109-181d9300-d9ed-11eb-8472-37105dffdb08.png">
   
4. 

   
<img width="581" alt="스크린샷 2021-06-30 오후 8 53 31" src="https://user-images.githubusercontent.com/57285121/123956034-3b444480-d9e5-11eb-926b-a27ce6db7a9e.png">
   

