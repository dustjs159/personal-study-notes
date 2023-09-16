💻 [AWS] ECS Task
=============================
# ECS Task
* 컨테이너를 시작하기 위한 config 정의

## Task Definition 생성 시 옵션
* Infra Structure 정의
    * Launch Type
        * AWS Fargate or EC2
    * OS : Linux x86/ARM or Windows
    * Network mode : awsvpc
    * Task Size : Task 실행에 필요한 컴퓨팅 파워
        * vCPU, Memory
    * Role
        * Task Role
        * Task Execution Role
    
