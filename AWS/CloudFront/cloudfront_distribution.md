💻 [AWS] CloudFront Distribtion
==============================
## CloudFront에서 Distribution?
* **Distribution**
  * 글로벌한 AWS의 인프라에서의 CDN 캐싱 서버(CDN의 구분 단위)
  * 여러 Edge Location에서 컨텐츠를 제공하기 위한 채널 (POP). Distribution 하나가 여러 Edge Location에서 컨텐츠를 제공

### 생성시 주요 옵션
* Origin 설정
  * S3, ELB 또는 Custom 등을 지정할 수 있으며 사용자에게 제공할 원본 컨텐츠가 위치한 Source.
  * Custom Origin에는 HTTP/HTTPS 서비스를 제공할 도메인을 입력하면 된다. S3의 Static Web Hosting Endpoint 같은..
* Origin Path
  * Client의 요청 URL의 경로에 따라 다른 컨텐츠를 제공하기 위한 옵션. 두 개의 Origin을 생성하고 각각 `example.com` 도메인에 대해 `/dev, /prod` 의 path가 설정되어 있을 경우에 `example.com/dev` 로 요청이 오면 `/dev` 내 경로의 컨텐츠를 전송하고 `example.com/prod` 로 요청이 오면 `/prod` 내 경로의 컨텐츠를 전송한다. (사용자의 요청에 대해 분기 처리를 위한 옵션)
* Name
  * Origin 이름 설정
* Add Custom Header
  * POP에서 Origin으로 요청을 전달할 때 추가로 Header를 붙여서 전달할 수 있는 기능. 언제 사용하는지는 잘 모르겠다.
* Origin Shield
  * REC와 유사하나 가용성 향상에 도움이 되는 캐싱 레이어


