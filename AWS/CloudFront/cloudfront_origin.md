💻 [AWS] CloudFront Origin
==============================
## CloudFront에서 Origin?
* **Origin** : 실제 컨텐츠가 존재하는 지점(S3, EC2, ELB 등)
  * Origin Request : CloudFront가 Origin에게 요청을 보내는 시점
  * Origin Response : Origin으로 부터 CloudFront에 응답이 오는 시점

### Origin Shield에 관하여
* Origin Shield
  * REC가 있는 리전에서만 지원되는 기능이며 REC와 유사한 캐싱 레이어이나 보안 측면에서 약간 차이점을 보인다.
  * REC와 유사한 점
    * POP과 Origin 사이의 캐싱 레이어를 추가함으로써 Cache Hit 확률을 높일 수 있다. 
    * Public Internet 망을 타는 것이 아닌 CloudFront POP ↔ REC / Origin Shield 사이에 AWS 인프라의 백본 망을 활용한 보안성 향상 
  * REC와 다른 점
    * ?
  * 추가 비용이 발생