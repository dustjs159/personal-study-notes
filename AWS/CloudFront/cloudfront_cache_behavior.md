💻 [AWS] CloudFront Cache Behavior
==============================
## CloudFront에서 캐싱 동작

설정 옵션

* Path Pattern
    * 경로에 따라 다른 캐싱 정책을 적용할 수 있는 설정 값.
        * 자주 바뀌는 컨텐츠의 경로에 대해서는 TTL을 낮게 설정하여 캐싱 기간을 줄이는 전략이 필요하다.
* Compress objects automatically
    * 사용자에게 전달되는 컨텐츠를 자동으로 압축하여 더 적은 용량으로 전송할 수 있도록 함 (default : yes)
* Viewer Protocol Policy
    * 사용자의 요청에 대한 처리 정책. Redirect HTTP to HTTPS이나 HTTPS Only를 쓰자. 웬만하면.
* Allowed HTTP methods
    * CloudFront POP에서 허용할 HTTP 메소드를 지정할 수 있음.
    * 사용자의 불필요한 HTTP 메소드를 제한하기 위해 사용 - 권고 : Read 수준의 GET, HEAD만 사용하는 것

## CloudFront TTL 설정
* **TTL(Time To Live)** : 캐싱이 존재하는 기간
  * TTL 시간이 지나면 캐싱 서버에서 캐싱이 제거되며 새로 Origin으로 부터 캐싱 정보를 가져옴
* Invalidation
  * 캐시 무효화(삭제)
  * 새로운 버전의 app을 배포할 경우 새 버전 app을 사용자에게 즉각적으로 서비스하고자 할 때, Invalidation 후 새 버전 app을 서비스 할 수 있도록 함.
* **Cache Policy**
  * 캐싱 정책
  * Policy 설정 옵션
    * Cache Key
    * TTL
    * Compression Support
* Cache Key
  * 어떤 컨텐츠를 캐싱할 지 결정
  * 기준 : 기본적으로 URL 단위. 부가적으로 Header, Cookie, Query String으로도 가능
* Behavior
  * CDN의 분기점이 되는 지점
  * 각 분기점마다 다른 캐싱 정책을 적용할 수 있음