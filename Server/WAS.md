WAS
=================================
## Summary
- Last Updated : 21.05.28 Fri    
- Updated by : 윤연선
-----------------------------------

# WAS(Web Application Server)
  
<img width="624" alt="스크린샷 2021-05-28 오후 4 08 05" src="https://user-images.githubusercontent.com/57285121/119944162-e4ef7a80-bfce-11eb-81f7-ac5169211ccb.png">
   
* 웹 서버로부터 오는 동적 컨텐츠 요청을 처리하는 서버
* **동적 컨텐츠 처리 가능** + 정적 컨텐츠도 처리 가능
* 주로 DB 서버와 같이 수행됨
* **웹 서버와 WAS를 같이 사용하여 정적 컨텐츠는 웹 서버가 처리하도록 하고 동적 컨텐츠 처리만 WAS가 담당하여 WAS 자체의 부하를 줄일 수 있도록 구성**

# WAS 종류

## Apache Tomcat
* Apache HTTP Server(웹 서버)와 Tomcat을 연동
* JAVA 언어로 개발할 수 있는 WAS
* Servlet/JSP Container : Servlet, JSP를 이용하여 동적인 데이터들을 처리하여 정적인 페이지로 생성해주는 소프트웨어 모듈
* Servlet   
> * JAVA를 사용하여 웹을 만드는 기술
   
<img width="773" alt="스크린샷 2021-05-28 오전 3 40 47" src="https://user-images.githubusercontent.com/57285121/119879735-7f67a380-bf66-11eb-8b8d-4606d6b052eb.png">
   
1. 클라이언트의 요청을 웹 서버가 받아서 웹 컨테이너에게 전달
2. 컨테이너가 스레드를 생성하고 요청 및 응답 객채(HttpServletRequest, HttpServletReques)를 생성하여 스레드에게 전달
3. 스레드, 요청 및 응답 객체 생성 후 클라이언트의 요청에 맞는 Servlet을 호출
4. 호출된 Servlet의 요청을 담당하는 스레드가 doGet(), doPost()호출
5. 호출된 doPost(), doGet() 메소드는 생성된 동적 컨텐츠를 Response 객체에 실어 컨테이너에 전달
6. 컨테이너는 Response객체를 HttpResponse형태로 전환하여 웹서버에 전달 하고 스레드 종료 + 요청 및 응답 객체 삭제

* 장점   
> * 무료   
* 단점   
> * 

## JEUS

## Websphere


