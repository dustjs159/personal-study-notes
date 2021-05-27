Web Server
=================================
## Summary
- Last Updated : 21.05.27 Thu    
- Updated by : 윤연선
-----------------------------------

# Web Server
   
<img width="541" alt="스크린샷 2021-05-27 오후 6 18 33" src="https://user-images.githubusercontent.com/57285121/119800669-f4f85300-bf17-11eb-8472-55fafe71d24d.png">
    
* 클라이언트의 요청(HTTP Request)을 받아 해당 요청에 대한 정보를 클라이언트에게 응답(HTTP Response)으로 반환해주는 서버

## 정적 페이지
* 클라이언트의 요청에 항상 같은 내용을 보여주는 웹 페이지
* 개발자에 의해 사전에 미리 준비된 페이지
* HTML, CSS 등으로만 구성
* Ex) 어느 사용자가 접속을 해도 항상 같은 내용만 표시되는 회사소개 페이지

## 동적 페이지
* 클라이언트의 요청에 따라 다른 내용을 보여주는 웹 페이지
* 미리 만들어진 웹 페이지가 아닌 클라이언트의 요청 시 만들어지는 웹 페이지
* Ex) 로그인 정보를 가져온 웹 페이지, 쇼핑몰 결제항목 등

# Web Server 종류
## Apache HTTP Server
   
<img width="701" alt="스크린샷 2021-05-26 오전 12 18 04" src="https://user-images.githubusercontent.com/57285121/119523591-d9763680-bdb7-11eb-953e-fc1fd4db7d83.png">
   
* 리눅스 기반 무료 오픈소스 웹서버(누구나 사용 가능)
* MPM(Multi Processing Module)방식으로 HTTP 요청을 처리
* PreFork MPM(멀티 프로세스 + 단일 스레드)
   
<img width="376" alt="스크린샷 2021-05-27 오후 6 41 21" src="https://user-images.githubusercontent.com/57285121/119804247-232b6200-bf1b-11eb-8010-2a47564ba8f5.png">
   
> * 미리 복수의 프로세스를 생성하여 클라이언트의 요청에 대비하는 멀티프로세스 방식   
> * 
> * 프로세스와 스레드가 1:1 

* Worker MPM(멀티 프로세스 + 스레드)

## Nginx

* 이벤트 중심

## IIs



