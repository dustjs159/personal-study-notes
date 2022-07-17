💻 [AWS] AWS CloudFront
===============
# 💡 Amazon CloudFront

* 사용자들에게 좀 더 빠르게 컨텐츠를 제공하기 위한 서비스 : **CDN(Content Delivery Network)** 
  * 여기서 컨텐츠란 HTML, CSS, .js 등으로 구성된 웹 페이지와 이미지, 동영상 등을 의미
* 전 세계 각지의 Edge Location에서 **캐싱**을 통해 빠른 속도로 사용자들에게 컨텐츠 제공
  * Edge Location : 컨텐츠가 캐싱되는 지점이자 사용자에게 컨텐츠가 제공되는 지점

## 📌 CloudFront 동작 방식

![스크린샷 2022-07-18 오전 12 36 12](https://user-images.githubusercontent.com/57285121/179405715-f26481fc-7f51-4ded-a3ff-988732951b0a.png)

1. 사용자가 웹 애플리케이션에 접근 (컨텐츠 요청)
2. DNS가 사용자가 요청한 지점으로 부터 가장 가까운 Edge Location으로 요청을 라우팅
3. CloudFront에 캐시가 있는 경우 사용자에게 캐시 전달   
  3-a. CloudFront에 캐시가 없다면, Origin(S3 버킷 or 웹 서버)에 사용자의 요청 전달   
  3-b. Origin은 CloudFront로 응답을 전달   
  3-c. CloudFront는 Origin에게 받은 응답을 사용자에게 전달

## 📌 CloudFront 주요 설정 및 개념

* Origin : 실제 컨텐츠가 존재하는 지점(S3, EC2, ELB 등)
* TTL(Time To Live)
  * 캐싱이 존재하는 기간
  * TTL 시간이 지나면 캐싱 서버에서 캐싱이 제거되며 새로 Origin으로 부터 캐싱 정보를 가져옴
* Invalidation : 무효화
* Distribution : CDN 캐싱 서버(CDN의 구분 단위)
* 사용자의 요청 지점과 본래 서버간 거리가 지리적으로 먼 경우에 요청 지점과 가까운 CDN 에을 통해 빠르게 컨텐츠 제공
  * 서버로 직접 요청하는 것이 아니기 때문에 서버의 부하를 줄일 수 있음
* Distributions 
* Viewer
* Behavior

## CORS
* CloudFront + S3 연동 웹 페이지 구성할 때 CORS 에러 허용

