💻 [AWS] AWS CloudFront
===============
# 💡 Amazon CloudFront

* 사용자들에게 좀 더 빠르게 컨텐츠를 제공하기 위한 서비스 : **CDN(Content Delivery Network)**
* 사용자의 요청 지점과 본래 서버간 거리가 지리적으로 먼 경우에 요청 지점과 가까운 CDN을 통해 빠르게 컨텐츠 제공 
  * 여기서 컨텐츠란 HTML, CSS, .js 등으로 구성된 웹 페이지와 이미지, 동영상 등을 의미
* 전 세계 각지의 Edge Location에서 **캐싱**을 통해 빠른 속도로 사용자들에게 컨텐츠 제공
  * Edge Location(POP) : 컨텐츠가 캐싱되는 지점이자 사용자에게 컨텐츠가 제공되는 지점
* 웹 서버로 직접 요청하는 것이 아니기 때문에 서버의 부하를 줄일 수 있음


## 📌 CloudFront 동작 방식

![스크린샷 2022-07-18 오전 12 36 12](https://user-images.githubusercontent.com/57285121/179405715-f26481fc-7f51-4ded-a3ff-988732951b0a.png)

1. 사용자가 웹 페이지에 접근 (컨텐츠 요청)
2. DNS가 사용자가 요청한 지점으로 부터 가장 가까운 Edge Location으로 요청을 라우팅
3. Edge Location에 캐시가 있는 경우 사용자에게 캐시 전달   
  3-a. Edge Location에 캐시가 없다면, Origin(S3 버킷 or 웹 서버)에 사용자의 요청 전달   
  3-b. Origin은 Edge Location로 응답을 전달   
  3-c. Edge Location는 Origin에게 받은 응답을 사용자에게 전달 + 캐시 저장

## 📌 CloudFront 주요 설정 및 개념

* Origin : 실제 컨텐츠가 존재하는 지점(S3, EC2, ELB 등)
  * Origin Request : CloudFront가 Origin에게 요청을 보내는 시점
  * Origin Response : Origin으로 부터 CloudFront에 응답이 오는 시점
* TTL(Time To Live)
  * 캐싱이 존재하는 기간
  * TTL 시간이 지나면 캐싱 서버에서 캐싱이 제거되며 새로 Origin으로 부터 캐싱 정보를 가져옴
* Invalidation
  * 캐시 무효화(삭제)
  * 비용 발생
* Distribution
  * CDN 캐싱 서버(CDN의 구분 단위)
  * 여러 Edge Location에서 컨텐츠를 제공하기 위한 채널. Distribution 하나가 여러 Edge Location에서 컨텐츠를 제공 
* Cache Key
  * 어떤 컨텐츠를 캐싱할 지 결정
  * 기준 : 기본적으로 URL 단위. 부가적으로 Header, Cookie, Query String으로도 가능
* Cache Policy
  * 캐싱 정책
  * Policy 설정 옵션
    * Cache Key
    * TTL
    * Compression Support
* Viewer
  * Viewer Request : CloudFront에 사용자의 요청을 보내는 시점
    * CloudFront는 뷰어의 정보를 헤더에 더해 Origin에 데이터를 전송하는데 이 때 헤더를 통해 확인할 수 있는 정보는 IP 주소, 국가, 도시, Timezone, 디바이스 타입(Desktop, Mobile 등) 등이 있다 
  * Viewer Response : CloudFront로 부터 사용자에게 응답이 오는 시점
* Behavior
* OAI(Origin Access Identity)
  * S3 버킷 내 오브젝트를 CloudFront를 통해서만 접근할 수 있도록 제한
  * S3 버킷 정책을 통해 CloudFront를 제외한 나머지 접근을 제한하여 사용자들의 버킷 직접 접근을 막음 
* Field Level Encryption
  * CloudFront ↔️ Origin 사이의 통신을 암호화
  * 공개키 암호화 방식으로 암호화
    * CloudFront에 Public Key가 있고, Origin에게 데이터 전송 시 Public Key로 암호화 하여 전송, Origin에서는 Private Key로 복호화
  * CloudFront가 Viewer와 HTTPS 통신을 지원하기에 CloudFront와 Origin간의 통신은 HTTP 통신을 하는 경우가 있는데, 이 때 CloudFront와 Origin간 거리가 멀 경우 탈취 가능성이 있기 때문에 암호화를 한다.

## 📌 CloudFront 동적 컨텐츠 처리

* CloudFront에서 정적/동적 컨텐츠는 URL 경로 패턴 매칭으로 분기 처리
* 정적 컨텐츠는 S3 버킷 내 CSS, HTML 등을 캐싱하여 컨텐츠 제공 속도 최적화 
* 동적 컨텐츠는 TCP Connection 유지, 파일 압축(Gzip 등)등을 통해 컨텐츠 제공 속도 최적화


![CloudFront](https://user-images.githubusercontent.com/57285121/180594680-d88161ba-13a0-4558-a797-d0d60c07d3bc.jpg)

## 📌 CloudFront에서 HTTPS 지원

![CloudFront](https://user-images.githubusercontent.com/57285121/180595009-6016e94c-8f7e-45aa-96bf-99d676772907.jpg)

* CloudFront에 ACM(AWS Certificate Manager)에서 발급받은 SSL/TLS 인증서를 적용하여 Origin의 웹 서버에서 따로 HTTPS를 적용하지 않고도 HTTPS를 적용할 수 있음

## CloudFront + S3 Static 웹 페이지 호스팅

* CORS 주의!
* CloudFront + S3 연동 웹 페이지 구성할 때 CORS 에러 허용

