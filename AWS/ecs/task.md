Amazon ECS Task
=============================
### 정의 
* 실행되는 컨테이너의 단위

### Task Definition 
* 태스크를 어떻게 실행할 것인가? 에 대한 정의.
* 태스크는 서비스에 의해 실행될 수도 있고 단독으로 실행될 수도 있음.
* 인프라 정의
    * Launch Type : 태스크를 실행할 인프라 유형 선택
        * Fargate, EC2, 
    * OS : Linux x86/ARM or Windows
    * Network mode : awsvpc
    * Task Size : Task 실행에 필요한 컴퓨팅 리소스
        * vCPU, Memory
    * Role
        * Task Role
        * Task Execution Role

### Task Role vs Task Execution Role
Task Definition을 생성하는 과정에서 선택할 수 있는 Role이 두 개가 있었는데 어떤 차이가 있을까?
* Task Role
    * 태스크 자체에 대한 권한. **태스크가 버킷에 오브젝트를 기록하거나 읽는 등의 작업을 위한 자격증명**이 필요할 때 Task Role을 사용하여 자격증명을 획득
* Task Execution Role
    * ECS 에이전트의 권한. 태스크 실행에 필요한 이미지를 업데이트하기 위해 ECR에 접근하기 위한 권한, awslogs 드라이버를 사용하기 위한 권한 등의 **태스크를 관리하기 위한 자격증명**이 필요할 때 Task Execution Role를 사용하여 자격증명을 획득 



    
