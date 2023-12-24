Amazon ECS
=============================
### 정의
* 도커라이징한 서비스를 배포/관리할 수 있는 컨테이너 오케스트레이션 도구

### 주요 개념
* Capacity : 서비스를 시작할 인프라 구성
    * 서비스를 어떤 인프라 위에서 동작하도록 할 것인가
    * 여기서 선택할 수 있는 인프라 유형은
        * EC2 인스턴스
        * ECS Fargate (serverless)
        * 그 외 온프레미스 장비 등
* Controller : 컨테이너에서 실행중인 서비스 배포/관리
* Provisioning : ECS를 사용하기 위한 AWS CLI, CDK, SDK 등을 의미

### 동작 원리
1. `docker image build`
    * local or CI/CD를 통해 docker 이미지 빌드
2. `image push`
    * 빌드한 이미지를 ECR(Elastic Container Registry)에 push
3. `create cluster`
    * cluster란 service or task가 실행되는 논리적인 단위
3. `create task definition`
    * 컨테이너를 실행할 이미지, 환경변수, 포트 등의 task 정의
4. `create service or task`
    * task definition을 기반으로 service or task 실행