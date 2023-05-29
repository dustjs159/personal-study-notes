💻 [AWS] EC2 Userdata
=============
* Userdata : EC2 인스턴스가 생성될 때 사용할 Bootstrap Script
* 인스턴스를 실행할 때 필요한 소프트웨어 설치 자동화 가능
  * nginx나 mysql 등

<img width="325" alt="스크린샷 2023-05-29 오후 3 28 25" src="https://github.com/dustjs159/Study/assets/57285121/6943c7fc-d041-4f14-acd9-dc88231e83f8">

* 패키지 업데이트, nginx 설치 및 시작하는 script를 미리 작성하여 인스턴스 내에서 실행할 작업 수행 가능
* User data에 입력한 Script는 Root 권한으로 실행되기에 따로 sudo 명령어를 작성할 필요 없음.
