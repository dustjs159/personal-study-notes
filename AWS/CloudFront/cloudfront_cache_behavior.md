💻 [AWS] CloudFront Cache Behavior
==============================
## CloudFront에서 캐싱 동작
* Cache Behavior
  * 컨텐츠 경로마다 다른 캐싱 정책을 적용할 수 있음

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
    * 사용자의 불필요한 HTTP 메소드를 제한하기 위해 사용
        * 정적 컨텐츠일 경우 Read 수준의 GET, HEAD만 사용하도록 하자.
        * 동적 컨텐츠일 경우 GET, HEAD 이외에도 POST, PUT 등의 메소드도 같이 사용할 수 있도록 한다.
* **Cache Policy** : 캐싱 정책
  * Policy 설정 옵션
    * Cache Key : 어떤 콘텐츠를 캐싱할지 결정한다. 그 기준은 기본적으로 URL 단위. 부가적으로 Header, Cookie, Query String으로도 가능
    * **TTL 설정**
    * Compression Support

<img width="520" alt="스크린샷 2023-04-12 오전 12 04 38" src="https://user-images.githubusercontent.com/57285121/231205686-4551bae6-4608-4e9e-8e42-679dd66ec465.png">

* Origin Request Policy
    * Cache Miss가 발생했을 때, CloudFront는 Origin에 요청을 전달하게 된다(Origin Request). 이 때 적용할 정책을 설정할 수 있다.
    * CloudFront가 Origin에게 추가로 전달할 Header 설정 가능 (ALB 연동하면서 애먹었던 부분...)
* Response headers policy
    * Origin 측에서 CloudFront의 요청에 대해 응답할 때(Origin Response) 적용할 정책
* Function 지정 가능
    * JavaScript 기반의 경량 함수 혹은 Lambda@Edge를 통해 이벤트 기반의 함수를 실행할 수 있음.
    * Lambda@Edge : Edge Location에서 실행되는 Lambda 함수.
    * Viewer Req/Res, Origin Req/Res 총 4개의 지점에 적용할 수 있음.
    
