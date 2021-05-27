WAS
=================================
## Summary
- Last Updated : 21.05.28 Fri    
- Updated by : 윤연선
-----------------------------------

# WAS(Web Application Server)
   
<img width="606" alt="스크린샷 2021-05-28 오전 3 33 03" src="https://user-images.githubusercontent.com/57285121/119878705-6ad6db80-bf65-11eb-9a55-1ecead75027d.png">
   
* 웹 애플리케이션을 실행시켜 필요한 기능을 수행하고 그 결과를 웹 서버에게 전달
* **동적 컨텐츠 처리 가능**
* Web Server + Web Container로 구성

## Web Container
* Servlet, JSP을 실행 가능한 소프트웨어
   
<img width="773" alt="스크린샷 2021-05-28 오전 3 40 47" src="https://user-images.githubusercontent.com/57285121/119879735-7f67a380-bf66-11eb-8b8d-4606d6b052eb.png">
   
1. 클라이언트의 요청을 웹 서버가 받아서 웹 컨테이너에게 전달
2. 컨테이너가 스레드를 생성하고 요청 및 응답 객채(HttpServletRequest, HttpServletReques)를 생성하여 스레드에게 전달
3. 스레드, 요청 및 응답 객체 생성 후 클라이언트의 요청에 맞는 Servlet을 호출
4. 호출된 Servlet의 요청을 담당하는 스레드가 doGet(), doPost()호출
5. 호출된 doPost(), doGet() 메소드는 생성된 동적 컨텐츠를 Response 객체에 실어 컨테이너에 전달
6. 컨테이너는 Response객체를 HttpResponse형태로 전환하여 웹서버에 전달 하고 스레드 종료 + 요청 및 응답 객체 삭제

# WAS 종류

## Tomcat

## JEUS

## Websphere


