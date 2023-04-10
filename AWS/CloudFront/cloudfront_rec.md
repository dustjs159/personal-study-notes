💻 [AWS] CloudFront REC
==============================

## REC - Regional Edge Cache
<img width="576" alt="스크린샷 2023-04-03 오후 10 58 14" src="https://user-images.githubusercontent.com/57285121/229531716-5fc3f69d-7edb-4d1a-af5b-8b24939462da.png">

* REC(Regional Edge Cache) : AWS에서 제공하는 계층형 캐시 - CloudFront Distribution (POP)과 Origin사이의 추가적인 캐싱 레이어.
  * **POP보다 Origin에 더 가까이 위치**하며 사용자가 POP에 요청을 했을 때 **POP에 캐시가 없다면 REC에 요청**을 하고 REC에도 캐시가 없다면 Origin에 요청하여 컨텐츠를 전달받는다.
  * POP보다 더 고성능의 캐싱 서버를 사용하여 이를 바탕으로 같은 리전 내 여러 POP들이 동일한 요청을 받았을 때, REC는 Origin으로부터 가져온 컨텐츠를 여러 POP에 공유할 수 있도록 캐싱한다.
    * 위 그림에서 두개의 POP (Edger Location)에서 하나의 REC에 요청을 전달하는 것을 볼 수 있다. (그리고 POP보다 크기도 더 크다.)
* REC는 CloudFront POP 생성시 내부적으로 자동 생성된다. (별도의 비용 없음)

REC 레이어가 추가된 CloudFront 캐시 응답 방식은 다음과 같다.

1. 사용자가 웹 페이지에 접근 (컨텐츠 요청)
2. DNS가 사용자가 요청한 지점으로 부터 가장 가까운 Edge Location으로 요청을 라우팅
3. Edge Location에 캐시가 있는 경우 사용자에게 Edge Location의 캐시 전달 => **POP Cache Hit**
4. Edge Location에 캐시가 없는 경우 REC으로 요청을 라우팅
5. REC에 캐시가 있는 경우 사용자에게 REC의 캐시 전달 => **REC Cache Hit**
6. REC에도 없으면 Origin에 사용자의 요청을 전달하고 결과를 받아 사용자에게 전달. + 캐시 저장 => **Cache Miss**