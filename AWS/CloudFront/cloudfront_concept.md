💻 [AWS] AWS CloudFront
====================
# Amazon CloudFront
* 사용자들에게 좀 더 빠르게 컨텐츠를 제공하기 위한 서비스 : **CDN(Content Delivery Network)**
* 사용자의 요청 지점과 본래 서버간 거리가 지리적으로 먼 경우에 요청 지점과 가까운 CDN을 통해 빠르게 컨텐츠 제공 
  * 여기서 컨텐츠란 정적인 `HTML`, `CSS`, `.js` 등으로 구성된 웹 페이지와 `.jpg`, `.png` 형식의 이미지, `.mp4` 형식의 동영상 뿐만 아니라 동적인 요청도 포함.
* 전 세계 각지의 Edge Location에서 **캐싱**을 통해 빠른 속도로 사용자들에게 컨텐츠 제공
  * Edge Location(POP) : 컨텐츠가 캐싱되는 지점이자 사용자에게 컨텐츠가 제공되는 지점
* 웹 서버로 직접 요청하는 것이 아니기 때문에 서버의 부하를 줄일 수 있음

## 사용자의 요청에 대한 CloudFront의 캐시 응답 방식
![스크린샷 2022-07-18 오전 12 36 12](https://user-images.githubusercontent.com/57285121/179405715-f26481fc-7f51-4ded-a3ff-988732951b0a.png)

CloudFront 캐시 응답 방식은 다음과 같다.

1. 사용자가 웹 페이지에 접근 (컨텐츠 요청)
2. DNS가 사용자가 요청한 지점으로 부터 가장 가까운 Edge Location으로 요청을 라우팅
3. Edge Location에 캐시가 있는 경우 사용자에게 캐시 전달 => **Cache Hit**   
  3-a. Edge Location에 캐시가 없다면 => **Cache Miss**, Origin(S3 버킷 or 웹 서버)에 사용자의 요청 전달   
  3-b. Origin은 Edge Location으로 응답을 전달   
  3-c. Edge Location는 Origin에게 받은 응답을 사용자에게 전달 + 캐시 저장

## CloudFront 요청/응답 동작
![CloudFront](https://user-images.githubusercontent.com/57285121/197563147-00c99569-86d4-44eb-a796-3e7052f866ec.jpg)

* **Viewer ↔️ Distribution ↔️ Origin**

Viewer
  * Viewer Request : CloudFront에 사용자의 요청을 보내는 시점
    * CloudFront는 뷰어의 정보를 헤더에 더해 Origin에 데이터를 전송하는데 이 때 헤더를 통해 확인할 수 있는 정보는 IP 주소, 국가, 도시, Timezone, 디바이스 타입(Desktop, Mobile 등) 등이 있다 
  * Viewer Response : CloudFront로 부터 사용자에게 응답이 오는 시점

Distribution
* 글로벌한 AWS의 인프라에서의 CDN 캐싱 서버(CDN의 구분 단위)
* 여러 Edge Location에서 컨텐츠를 제공하기 위한 채널. Distribution 하나가 여러 Edge Location에서 컨텐츠를 제공

Origin
  * 실제 컨텐츠가 존재하는 지점(S3, EC2, ELB 등)
    * Origin Request : CloudFront가 Origin에게 요청을 보내는 시점
    * Origin Response : Origin으로 부터 CloudFront에 응답이 오는 시점


## CloudFront 동적 컨텐츠 처리
![CloudFront](https://user-images.githubusercontent.com/57285121/180594680-d88161ba-13a0-4558-a797-d0d60c07d3bc.jpg)

* CloudFront에서 정적/동적 컨텐츠는 URL 경로 패턴 매칭으로 분기 처리
* 정적 컨텐츠는 S3 버킷 내 CSS, HTML 등을 캐싱하여 컨텐츠 제공 속도 최적화 
* 동적 컨텐츠는 TCP Connection 유지, 파일 압축(Gzip 등)등을 통해 컨텐츠 제공 속도 최적화