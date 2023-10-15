Proxy
=================================
## Summary
- Last Updated : 21.06.02 Wed   
- Updated by : 윤연선
-----------------------------------

# Proxy Server
* 클라이언트와 서버 사이에서 요청과 응답을 전달해 주는 서버
* PC와 외부 인터넷 사이의 징검다리 역할을 함
* 캐시를 통해 자원들을 저장할 수 있음
* Proxy Server를 거치는 요청 및 응답을 확인할 수 있음(Filter) : 보안성 향상, 로그 확인 가능
* Proxy Server로 넘어온 데이터를 조작할 수 있음(Trancode) : 데이터 압축, 언어 변환
* 클라이언트의 요청에 있어서 불필요한 부분은 걸러내고 서버에게 전송
   
<img width="532" alt="스크린샷 2021-05-17 오후 11 21 09" src="https://user-images.githubusercontent.com/57285121/118504544-91776400-b766-11eb-9dc8-ddb6188ba7aa.png">
   
# Forward Proxy
  
<img width="582" alt="스크린샷 2021-06-02 오전 2 57 25" src="https://user-images.githubusercontent.com/57285121/120369470-45274900-c34e-11eb-8e8e-b838bed89467.png"> 
   
* 클라이언트와 가까운 곳에 위치한 Proxy Server   
* 클라이언트가 웹 사이트에 연결하려고 요청을 보내면 서버에 직접 요청을 전송하는 것이 아니라 Forward Proxy가 요청을 받아서 웹 사이트에 연결 후 결과를 클라이언트에게 전달

* 캐싱
> * 전송 시간 절약 + 응답 속도 향상   
> * 불필요한 외부전송X   
> * 외부 요청 감소(네트워크 과부하 방지)  

* 익명성
> * 클라이언트가 보낸 요청을 숨김   
> * 서버가 받은 요청을 누가 보냈는지 알지 못하게 함   


# Reverse Proxy
   
<img width="604" alt="스크린샷 2021-06-02 오전 2 57 56" src="https://user-images.githubusercontent.com/57285121/120369525-5708ec00-c34e-11eb-929f-73fd9a7e0001.png">
   
* 서버와 가까운 곳에 위치한 Proxy Server
* 클라이언트가 웹 사이트에 리소스를 요청하면 Reverse Proxy는 요청을 받아서 내부 서버에서 리소스를 받은 후에 클라이언트에게 리소스 전달
* 클라이언트는 접근하고자 하는 목적지 서버가 최종 목적지가 되는 것이 아니라 Reverse Proxy가 최종 목적지가 됨

* 캐싱
> * 응답 속도 향상   
 
* 보안성
> * 클라이언트 측에서는 서버들의 IP 주소를 직접 알지 못하기 때문에 Reverse Proxy에 요청을 보내고, Reverse Proxy는 자신이 알고있는 서버에게 요청을 전송.(클라이언트는 Reverse Proxy가 실제 서버라고 인식)   
> * 실제 서버의 IP가 노출되지 않음   

* 로드밸런싱
> * 서버의 부하 분산   


