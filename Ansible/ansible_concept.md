Ansible 기초 개념
==================

* 코드로 인프라를 관리할 수 있는 오픈소스 기반 IaC(Infrastructure as Code) 도구
* 다수의 서버를 운영하다 보면 정기적인 OS 업데이트나 공통으로 적용이 필요한 Config 파일을 배포해야 하는 경우가 있는데, 이 때 일일이 서버에 접속하지 않고 한번에 필요한 작업을 수행할 수 있음

## Ansible 운영 구조
* Control Node (Master)
    * Ansible이 설치된 서버. 
    * Bastion Host나 Jump Server같은 경유지 서버를 통해 접근할 수 있도록 운영하고 있는 경우 Bastion Host가 Control Node가 될 수 있다.
* Managed Node (Slave)
    * Control Node의 관리 대상 서버. (Host)
    * Managed Node에는 Ansible이 설치되지 않는다.
* Inventory
    * Control Node가 제어할 Managed Node의 목록
* Playbook
    * Managed Node가 작업할 목록을 작성한 파일
    * `yaml` 형식으로 작성