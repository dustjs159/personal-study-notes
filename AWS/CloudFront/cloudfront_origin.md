💻 [AWS] CloudFront Origin
==============================
## CloudFront에서 Origin?
* **Origin** : 실제 컨텐츠가 존재하는 지점(S3, EC2, ELB 등)
  * Origin Request : CloudFront가 Origin에게 요청을 보내는 시점
  * Origin Response : Origin으로 부터 CloudFront에 응답이 오는 시점

### Origin생성시 주요 옵션

CloudFront POP을 생성하기 위해 지정하는 Origin 설정

* Origin
  * S3, ELB 또는 Custom 등을 지정할 수 있으며 사용자에게 제공할 원본 컨텐츠가 위치한 Source.
  * Custom Origin에는 HTTP/HTTPS 서비스를 제공할 도메인을 입력하면 된다. S3의 Static Web Hosting Endpoint 같은..
* Origin Path
  * Client의 요청 URL의 경로에 따라 다른 컨텐츠를 제공하기 위한 옵션. 두 개의 Origin을 생성하고 각각 `example.com` 도메인에 대해 `/dev, /prod` 의 path가 설정되어 있을 경우에 `example.com/dev` 로 요청이 오면 `/dev` 내 경로의 컨텐츠를 전송하고 `example.com/prod` 로 요청이 오면 `/prod` 내 경로의 컨텐츠를 전송한다. (사용자의 요청에 대해 분기 처리를 위한 옵션)
* Name
  * Origin 이름 설정
* Add Custom Header
  * POP에서 Origin으로 요청을 전달할 때 추가로 Header를 붙여서 전달할 수 있는 기능. 언제 사용하는지는 잘 모르겠다.
* Origin Shield

### Origin Shield에 관하여

<img width="975" alt="스크린샷 2023-04-10 오후 11 42 15" src="https://user-images.githubusercontent.com/57285121/230924126-415d5e5d-33fa-451d-95f4-ff1ce262ee61.png">
(예시)

* CloudFront POP, REC외에 또 다른 계층형 캐시
* Origin Shield는 REC와 Origin 사이에 위치한다. Origin Shield 기능을 활성화할 경우 REC의 모든 요청이 Origin Shield를 통과하게 되어 Origin의 부하를 줄여줄 수 있고 캐시 적중률을 향상시킬 수 있음.
* **비용 발생**


