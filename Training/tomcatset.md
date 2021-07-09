Tomcat Install & Set
=================================
## Summary
- Last Updated : 21.07.09 Fri    
- Updated by : 윤연선
---------------------------------
## Tomcat 설치과정과 구성환경 및 실습 테스트
* 본 글은 CentOS 8 환경에서 작성했습니다. 
---------------------------------

# Tomcat 설치하기
1. JDK 설치
> *  ``$ yum install java-1.8.0-openjdk``   
> * ``$ yum install java-1.8.0-openjdk-devel``
* 이렇게 되면 /usr/bin경로에 java 바이너리 파일이 생성됨

2. 환경변수 등록
* /etc/profile 파일에 다음과 같이 등록
   
<img width="640" alt="스크린샷 2021-07-09 오후 9 18 41" src="https://user-images.githubusercontent.com/57285121/125076740-3e34e880-e0fb-11eb-8675-add5ea5ab73f.png">
   
* 설정 후 ``$ source profile``

3. Tomcat 설치
* Tomcat 8.5.69버전 설치
* /usr/local 경로에서 설치 진행
* ``$ cd /usr/local``

4. Tomcat 홈페이지에서 wget 명령어로 사용 가능한 최신 버전 압축파일 다운로드   
> * 설치 링크 : https://tomcat.apache.org/download-80.cgi   
> * 설치 명령어 : ``$ wget https://mirror.navercorp.com/apache/tomcat/tomcat-8/v8.5.69/bin/apache-tomcat-8.5.69.tar.gz``   
   
<img width="748" alt="스크린샷 2021-07-09 오전 2 00 18" src="https://user-images.githubusercontent.com/57285121/124962298-6bc95580-e059-11eb-8981-a1cb16c1fa72.png">
   
5. 압축 해제 및 경로 변경
* 확장자가 .tar.gz로 되어있는 압축파일 해제      
> * 압축 해제 명령어 : ``$ tar -xvf <압축파일>``   

5-1. 압축 해제한 디렉토리의 경로를 변경   
> * ``$ mv apache-tomcat-8.5.69 /usr/local/tomcat``   

6. tomcat 설정 확인 및 환경변수 설정
* 마지막 줄에 URIEncoding="UTF-8" 추가
   
<img width="405" alt="스크린샷 2021-07-09 오후 9 27 32" src="https://user-images.githubusercontent.com/57285121/125077798-7ab51400-e0fc-11eb-8060-bc3cb03f0e0c.png">
   
6-1. 환경 변수 설정
* /etc/profile
* CATALINA_HOME에 대한 환경변수 추가
   
<img width="757" alt="스크린샷 2021-07-09 오후 9 32 49" src="https://user-images.githubusercontent.com/57285121/125078342-37a77080-e0fd-11eb-84e8-82e092fa0c04.png">
   
* 설정 후 ``$ source profile``

7. 실행 테스트
* ``$ ./startup.sh``
   
<img width="754" alt="스크린샷 2021-07-09 오후 5 21 23" src="https://user-images.githubusercontent.com/57285121/125047586-17b28580-e0da-11eb-9f20-b784153df3d6.png">
   
7-1. 포트번호 확인
* ``$ cd /apache-tomcat/conf``
* server.xml 파일의 포트 확인
   
<img width="412" alt="스크린샷 2021-07-09 오후 5 42 47" src="https://user-images.githubusercontent.com/57285121/125050620-146cc900-e0dd-11eb-9d1f-e3b2bc1941ad.png">
   
> * 포트번호 8080(tomcat의 default 포트 번호)확인   

7-2. 방화벽 설정
* firewalld를 통해 8080포트 접속 허용   
> * ``$ firewall-cmd --permanent --add-port=8080/tcp``   
> * ``$ firewall-cmd --reload``
   
<img width="616" alt="스크린샷 2021-07-09 오후 5 53 51" src="https://user-images.githubusercontent.com/57285121/125052157-a0cbbb80-e0de-11eb-95f5-7aa32494fc6a.png">

7-3. 웹에서 접속
* <ip 주소>:8080으로 접속
   
<img width="895" alt="스크린샷 2021-07-09 오후 9 37 56" src="https://user-images.githubusercontent.com/57285121/125078861-eea3ec00-e0fd-11eb-91c2-efa60400de6b.png">
      
