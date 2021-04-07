HTTP / HTTPS
====================================
HTTP(HyperText Transfer Protocol)
------------------------------------
##* 정의   
1. 웹상에서 클라이언트와 웹서버간 통신을 위한 프로토콜 중 하나
2. Port번호는 80번을 사용하고 클라이언트의 요청(Request)과 서버의 응답(Response)으로 구성
3. 클라이언트가 http를 이용해 서버에 웹 페이지의 정보를 요청하면 서버는 이 요청에 응답하여
정보제공   

##* 연결 및 해제 과정   
1. 클라이언트는 웹 브라우저에 도메인 이름을 입력
2. 웹 브라우저는 DNS서버로 가서 도메인 이름을 IP주소로 변환
3. 변환한 IP주소에 3 Way Handshake를 통해 해당 웹 서버에 연결
4. 데이터 전송 완료 후 4 Way Handshake를 통해 연결 종료   

##* 통신 과정   
1. 클라이언트가 서버에 Request 메시지 전송
2. 서버는 클라이언트의 Request 메시지를 확인 후 클라이언트에게 Response 메시지 전송   

##* Request 메시지   
1. 시작줄 

 