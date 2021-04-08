HTTP / HTTPS
====================================
HTTP(HyperText Transfer Protocol)
------------------------------------
### 정의   
1. 웹상에서 클라이언트와 웹서버간 통신을 위한 프로토콜 중 하나
2. Port번호는 80번을 사용하고 클라이언트의 요청(Request)과 서버의 응답(Response)으로 구성
3. 클라이언트가 http를 이용해 서버에 웹 페이지의 정보를 요청하면 서버는 이 요청에 응답하여
정보제공   

### 연결 및 해제 과정   
1. 클라이언트는 웹 브라우저에 도메인 이름을 입력
2. 웹 브라우저는 DNS서버로 가서 도메인 이름을 IP주소로 변환
3. 변환한 IP주소에 3 Way Handshake를 통해 해당 웹 서버에 연결
4. 데이터 전송 완료 후 4 Way Handshake를 통해 연결 종료   

### 통신 과정   
1. 클라이언트가 서버에 Request 메시지 전송
2. 서버는 클라이언트의 Request 메시지를 확인 후 클라이언트에게 Response 메시지 전송   

## Request 메시지   
시작줄, Header, Body로 구성   
1. 시작줄 : HTTP Method + 요청 대상(주로 URL) + HTTP 버전
> HTTP Method
>> GET : 데이터 요청 / POST : 데이터 입력   
>> PUT : 데이터 갱신 / DELETE : 데이터 삭제   
>> HEAD : 웹 서버의 정보 또는 정상 작동 여부 확인시 사용   
>> OPTIONS : 웹 서버가 지원하는 메소드 종류 확인   
> 요청 대상 - 주소의 URL
>> origin형식 : 끝에 '?'와 쿼리 문자열이 붙는 절대경로   
>> absolute형식 : 완전한 URL형식   
> HTTP 버전 - HTTP/1.1, HTTP/2.0 
>> HTTP/1.1은 기본적으로 연결당 하나의 요청과 응답을 처리   
따라서 동시 전송 문제와 다수의 리소스 처리 속도 문제 발생   
>> HTTP/2.0은 이러한 HTTP/1.1의 문제점을 개선하고자 등장   
- Multiplexed Steams : 한 연결에 여러 메시지를 동시에 송,수신 가능
- Stream Prioitization : 요청 리소스 간 의존관계 설정
- Server Pu


