💻 [AWS] CloudFront TTL
==============================
## CloudFront에서 TTL 설정을 통해 효율적인 CDN 구축
* **TTL(Time To Live)** : 캐싱이 존재하는 기간
  * 컨텐츠 경로마다 다른 캐싱 정책을 적용할 수 있음

<img width="815" alt="스크린샷 2023-04-13 오후 11 11 04" src="https://user-images.githubusercontent.com/57285121/231786281-1b9db793-61f0-4721-87e2-8a7ac679e981.png">

* 컨텐츠마다 각각 다른 캐싱 정책을 설정하기 위해 custom 정책을 생성하려고 하다보니, 정책의 TTL을 설정할 때 Min/Max TTL과 Default TTL이 있는데 문득 든 생각이 Min TTL과 Default TTL중 어떤 것이 먼저 적용되는지 궁금했다.
    * Minimum TTL : 최소 캐시 적용 기간
    * Maximum TTL : 최대 캐시 적용 기간
    * Default TTL : 기본 캐시 적용 **(Cache-Control Header가 없는 경우에 적용)**