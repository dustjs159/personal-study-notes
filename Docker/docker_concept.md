💻 [Docker] Concept
==================
# Docker 개념
* 개발자들의 서비스 개발이 완료되어 상용에 배포해야할 때 새로운 서버를 만들고 서비스가 실행되기 위한 환경(node, python 설치 등등)을 설정하는 것은 상당히 번거로운 일이다. 
* 작업해야할 서버의 수가 많지 않을 경우에는 직접 수작업으로 설치해도 큰 문제가 없지만, 설치해야 할 서버의 수가 수백, 수천대일 경우에는 수작업으로 설치하는 것이 매우 귀찮은 일이다.
* 이 때 Docker를 사용해서 서비스가 동작하기 위해 필요한 도구(라이브러리, 패키지, 코드 등)를 한번에 묶어 **컨테이너**라는 단위에 담아 배포하면 Production 스테이지에 대한 배포의 수고를 조금이나마 덜 수 있다. 

### VM과 Docker의 가상화 방식 비교
* VM의 가상화 방식은 물리적인 하드웨어 위에서 작동하는 hypervisor를 통해 Host OS 위에 가상의 **Guest OS**를 만드는 방식
* Docker의 가상화 방식은 물리적인 장비 위에서 작동하는 소프트웨어 Docker Engine을 통해 가상의 **Container** 를 만드는 방식

![docker-vm](https://user-images.githubusercontent.com/57285121/216800878-ad7ffca0-7a86-4164-a108-1c43b8bb6d1e.jpeg)

* VM의 가상화 방식은 Host OS의 모든 하드웨어 자원을 공유하기 때문에 무겁고 느리다는 단점이 존재
  * 당연히 OS 전체를 구성해야 하니 무겁고 느릴 수 밖에 없다.
* 이러한 단점을 극복하기 위해 Docker 엔진을 통해 상대적을 경량화된 컨테이너를 생성.
  * VM 보다 훨씬 가볍고 빠름

## Docker LifeCycle

![docker-lifecycle](https://user-images.githubusercontent.com/57285121/214293603-2f8a14ea-f6cc-4cb2-9930-3acda4dc3cab.png)

* `docker create` / `docker run` 차이점
  * `docker create` 는 컨테이너만 만들고 그 이후에 특정 이미지를 지정하고 `docker start` 를 해야 실행된다.
  * `docker run` 은 컨테이너를 생성함과 동시에 실행까지 한다.
    * 물론 옵션에 컨테이너에서 실행할 이미지(pull로 받아온)를 지정해줘야 한다.