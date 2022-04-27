💻 [Network] HTTP
=====================

# 💡 HTTP(HyperText Transfer Protocol)
* HyperText ?
  * 일반적인 책을 읽을 때는 순서대로 책을 읽음(순차적인 정보습득)   
  * HyperText는 이러한 순차적 방법으로 정보를 습득하는 것이 아니라 문서들을 넘나들며 원하는 정보를 습득(비순차적 정보습득)
* 클라이언트 - 서버 구조로써 클라이언트와 서버 간 HyperText를 주고 받기 위한 프로토콜  
* Port번호는 80번을 사용하고 클라이언트의 요청(Request)과 서버의 응답(Response)으로 구성   
* 클라이언트가 HTTP를 이용해 서버에 웹 페이지의 정보를 요청하면 서버는 이 요청에 응답하여 정보제공
   
![http](https://user-images.githubusercontent.com/57285121/116813732-3b17fc00-ab90-11eb-9229-15149a7d1e61.png)   
   
## 📌 HTTP 주요 특징

* Client - Server Model
  * Client : Request의 주체
  * Server : Response의 주체
* Connectionless : 연결을 매번 끊고 새로 생성
  * 서버는 Response 후 Connection 종료
* Stateless : 상태 비저장
  * 서버는 이전의 클리이언트의 Request를 저장하지 않음
* Connectionless, Stateless 특성을 극복하기 위해 Cookie 를 만들어 저장


## 📌 HTTP 통신 과정
1. 클라이언트가 웹 브라우저에 방문하고자 하는 사이트의 URL 주소 입력
2. DNS 서버에서 클라이언트가 입력한 URL 주소에 대한 웹 서버의 IP 주소를 반환
3. 웹 서버와 TCP 3 way-handshake 과정을 통해 세션 수립
4. 클라이언트의 요청(HTTP Request)을 서버로 전달
5. 서버는 클라이언트의 요청에 대해 응답(HTTP Response)을 클라이언트에게 전달
6. 데이터 통신 종료 후 TCP 4 way-handshake 과정을 통해 세션 해제

## 📌 HTTP Request
* 요청라인 + 헤더(Header) + 본문(Body)으로 구성 

1. 요청라인 : HTTP Request Method + 요청URL + HTTP 버전

* HTTP Request Method   
  * GET : 데이터 요청   
  * POST : 데이터 입력   
  * PUT : 데이터 갱신   
  * DELETE : 데이터 삭제   
  * HEAD : 웹 서버의 정보 또는 정상 작동 여부 확인시 사용   
  * OPTIONS : 웹 서버가 지원하는 메소드 종류 확인   
* 요청 URL   
  * HTTP 요청이 전송되는 목표 주소   
* HTTP 버전   
  * HTTP/1.1, HTTP/2.0등 HTTP의 버전   

2. 헤더(Header)

* 요청에 대한 추가정보가 담겨있음
  * Host : 요청하는 호스트에 대한 호스트명 및 포트번호
  * User-Agent : 요청을 보내는 클라이언트의 소프트웨어 정보
  * Accept : 클라이언트가 원하는 미디어 타입(image, jpeg 등) 및 우선순위
  * Connection : 해당 요청이 끝난 후 클라이언트와 서버간의 연결을 계속 유지할 것인
지 끊을 것인지 알려주는 헤더(HTTP 요청 때마다 네트워크 연결을 새로 만드는 건 번>거롭기 때문에 요청이 계속되는 한 처음 연결을 재사용하는 것이 바람직)
  * Referer : 바로 직전에 머물렀던 웹 주소
  * Content-Length : 요청이 보내는 메시지 body의 총 사이즈 정보

3. 본문(Body)

* 요청이 전송하는 데이터를 담고있는 부분. Request Method가 GET일때는 비어있고 POST나 PUT일 때 채워짐

## 📌 HTTP Response
* 응답 상태 라인+헤더(Header)+본문(Body)으로 구성   

1. 응답 상태 라인: HTTP 버전 + 상태 코드(Status Code) + 상태 메시지(Status Text)

* HTTP 버전
  * HTTP/1.1 / HTTP/2.0   
* **상태 코드(Status Code)**
  * 1xx : 조건부 응답(요청을 받았고 작업을 계속 진행중)   
  * 2xx : 성공(클라이언트가 요청한 동작을 수신하고 이해하여 성공적으로 처리했음)   
  * 3xx : 리다이렉션 완료(클라이언트는 요청을 마치기 위해 추가 동작 필요)   
  * 4xx : 요청 오류(클라이언트에 오류가 있음)   
  * 5xx : 서버 오류(서버가 요청을 완벽히 수행하지 못함)
* 상태 메시지(Status Text)
   
|응답코드|상태 메시지|
|------|---|
|100|Continue(클라이언트로 부터 일부 요청을 받았고 나머지 정보를 계속 요청) |
|101|Switch Protocol|
|102|Processing(요청을 처리하고 있긴 하지만 제대로된 응답을 할 수 없는 상태)|
|200|OK(성공적으로 처리 완료)|
|201|Created(요청을 성공적으로 처리하여 리소스가 만들어 짐)|
|202|Accepted(웹 서버가 명령을 수신)|
|203|Non-Autohritative Information(서버가 클라이언트 요청 중에서 일부만 전송)|
|204|No Content(클라이언트 요청을 처리했으나 전송할 데이터가 없음)|
|301|Moved Permannetly(컨텐츠가 영구적으로 이동)|
|304|Not Modified(요청한 리소스를 재전송할 필요가 없음)|
|400|Bad Request(잘못된 요청)|
|401|Unauthorized(권한 없음)|
|402|Payment Required(결제 필요)|
|403|Forbidden(요청거부)|
|404|Not Found(찾을 수 없음)|
|408|Request Timeout(요청시간초과)|
|410|Gone(리소스 사라짐)|
|500|Internal Sever Error(내부 서버 에러)|
|502|Bad Gateway(게이트웨이 불량)|
|503|Service Temporaily Unavailable(일시적 서비스 이용 불가)|
|504|Gateway Timeout(게이트웨이 시간 초과)|
   
2. 헤더(Header)
* 요청에 대한 추가정보가 담겨있음   
* Reqeust Header와 동일. 단, User-Agent대신 Server가 사용(Server 소프트웨어 정보)   

3. 본문(Body)
* Request Body와 동일. 전송할 데이터가 없으면 비어 있음   

## 📌 HTTP 버전   
* 크게 HTTP/1.1과 HTTP/2.0 두 가지로 나뉘어짐   
* HTTP/1.1은 기본적으로 연결당 하나의 요청과 응답을 처리. 따라서 동시 전송 문제와 다수의 리소스 처리 속도 문제가 발생   
* HTTP/2.0은 이러한 HTTP/1.1의 문제점을 개선하고자 등장
  * Multiplexed Steams : 한 연결에 여러 메시지를 병렬로 동시에 송,수신 가능(응답 순서 상관없음)   
  * Stream Prioitization : 요청 리소스(이미지, 동영상 등) 간 우선순위를 설정하여 속도 문제 개선   
  * Server Push : 서버 측에서 클라이언트가 요청하지도 않은 리소스를 보냄(클라이언트의 요청을 최소화 해서 성능 향상을 기대할 수 있음)   
  * Header Compression : 헤더 정보 압축. 여러 요청을 보낼 때 중복된 헤더를 검출하고 하나의 헤더만 전송.   

## 📌 HTTP Keep-Alive
* HTTP는 클라이언트의 요청과 서버의 응답 후 연결이 종료됨
* 클라이언트의 요청이 많아지면 네트워크의 병목현상 발생
* HTTP에서 세션의 수립과정에서 Keep-Alive의 Timeout을 정해놓고 해당 시간동안에는 연결을 끊지 않고 유지함
* 네트워크 병목현상을 어느정도 해소할 수 있음
* Keep-Alive Timeout 동안 연결을 유지하고, Timeout이 지난 후에도 요청이 없으면 세션 해제
* TCP Keep-Alive의 타이머가 설정되어 있어도 HTTP Keep-Alive의 Timeout이 설정되어 있다면 HTTP Keep-Alive의 Timout에 맞춰 연결을 종료함(우선 순위가 TCP Keep-Alive의 타이머보다 HTTP-Keep Alive의 Timeout이 더 우선)
* TCP Keep-Alive가 3-way handshake 과정에서 설정한 타이머 값 주기로 서버와 클라이언트 중 연결을 원하는 쪽에서 Keep-Alive를 요청.
* HTTP Keep-Alive는 설정한 Timeout이 종료되면 연결을 종료. 주기적으로 Keep-Alive를 설정하기 위해서는 Timeout이 종료될 때마다 다시 Timeout을 설정하여 연결을 해야함
* 웹 애플리케이션 측면에서 웹 브라우저와 웹 서버간 최대한 연결을 유지하는 것이 주 목적

 
# HTTPS(HyperText Transfer Protocol Secure)
* HTTP의 보얀 취약점을 개선하기 위해 보안 기능을 추가한 프로토콜   
* 기존 HTTP에 SSL(Secure Socket Layer)을 사용   
* 포트 번호는 443번
* **SSL/TLS 인증서**
> * 보호받아야 할 개인정보를 제 3자가 알아볼 수 없도록 암호화   
> * 접속한 웹 사이트가 신뢰할 만한 사이트인지 알려줌   

## 📌 HTTPS 통신 과정
   
<img width="712" alt="스크린샷 2021-05-15 오전 3 42 21" src="https://user-images.githubusercontent.com/57285121/118314774-90a8bd00-b52f-11eb-937a-dc909ccb4085.png">   
   
* 대칭키 암호화 방식과 공개키 암호화 방식을 혼합해서 사용하는 SSL으로 데이터를 암호화하여 안전하게 데이터 전달이 가능
* SSL인증서를 통해 방문한 사이트가 신뢰할 수 있는 사이트임을 확인

## 인증서
* 정의   
> * 클라이언트와 서버 간 통신의 안정을 보증해주는 문서   
> * 클라이언트가 서버에 접속하게 되면 서버는 클라이언트에게 이 인증서를 전달해서 신뢰를 얻게 됨   
* 종류
> * DV(Domain Validation) : 도메인 소유/관리에 대한 검사인 DCV검사만 확인 후 발급되는 인증서. 가격이 저렴하고 CA에서 규정한 Email/DNS/HTTP 인증 방법만 통과하면 발급 완료. 소요시간은 2~5분   
> * OV(Organization Validation) : 도메인 소유/관리 권한 DCV 검사 뿐만 아니라 해당 인증서를 신청한 기관에 대한 실체 여부까지 확인후 발급되는 인증서. 해당 기관 담당자의 재직증명도 필요하고 DV에 비해 가격도 더 비싸다   
> * EV(Extended Validation) : 가장 높은 인증수준. DV와 OV의 과정을 모두 거치고 추가적으로 사업자 등록증으로 도메인 소유주와 사업자 등록증 상의 업체가 일치하는지 확인하고 전화통화도 해야함. 주소창이 녹색으로 변하며 금융사이트 및 관공서에서 사용됨
* 발급기관
> * CA(Certification Authority) : 디지털 인증서를 발급하는 기관. 공개키 기반 구조   
> * RA(Registration Authority) : 디지털 인증서에 관한 사용자 요청을 검증하여 CA가 그것을 발급하도록 알려주는 네트웍 상의 기관. 사용자들이 정보를 보다 안전하게 교환할 수 있는 시스템인 공개키 기반구조의 일부. 디지털 인증서는 전자서명과 메시지의 암,복호화에 사용되는 공개키를 담고있음   
> * VA(Validation Authority) : 디지털 인증서 유효성을 검증

