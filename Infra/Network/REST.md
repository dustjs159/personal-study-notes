REST API
========================
## Summary
- Last Updated : 21.05.25 Tue   
- Updated by : 윤연선
-----------------------------------

# API(Application Programming Interface)
* 프로그래밍 언어마다 원하는 결과를 출력하기 위해서 각각 다른 방식을 사용
* 이 때 각각 다른 언어로 데이터를 주고받으면 서로 해석이 불가능해짐
* 그래서 서로 규약을 맞춰주고 해당 규약으로 통신을 해야함


# REST(Representational State Transfer) API
* HTTP를 기반으로 다른 응용프로그램들과 통신할 수 있는 API
  
<img width="738" alt="스크린샷 2021-05-25 오후 9 53 52" src="https://user-images.githubusercontent.com/57285121/119501294-b3df3200-bda3-11eb-9525-0b503e243e09.png">
   
* 웹 페이지의 리소스들을 URI로 표현
   
<img width="691" alt="스크린샷 2021-05-25 오후 10 17 05" src="https://user-images.githubusercontent.com/57285121/119504459-f35b4d80-bda6-11eb-8cb2-9f915b417df8.png">
   
* 웹 페이지의 리소스들을 Create, Read, Update, Delete하기 위해 HTTP Method를 이용
* Create - POST
* Read - GET
* Update - PUT(전체 리소스 수정) / PATCH(일부 리소스 수정)
* Delete - DELETE


