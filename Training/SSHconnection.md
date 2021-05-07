Remote Server Connection by SSH Protocol
===============================================
Local(Windows)에서 SSH프토토콜을 이용해 원격 접속 해보자
-----------------------------------------------

# SSH Server 접속

* 선행 조건
> * 22번 포트가 방화벽에서 열려있어야 함
> * SSH 서버가 작동중이여야 함
> * SSH 프로토콜로 SSH서버에 접속할 수 있는 SSH클라이언트가 필요


# SSH Server 설치

* 대부분 최신의 리눅스 배포판들은 SSH 서버가 탑재(설치)되어 있음
* 만약 설치가 안되어 있다면 OpenSSH(SSH 프로토콜을 사용하여 원격 접속을 위한 프로그램)설치
> * CentOS, RedHat : ```yum install openssh-server```   
> * Ubuntu, Debian : ```apt-get install openssh-server```   
* 잘 설치가 되었는지 확인 : ```which sshd```   
![ssh1](https://user-images.githubusercontent.com/57285121/115655878-18efd400-a36f-11eb-83e6-821f19b2e900.PNG)

# SSH Server 작동

* SSH의 포트번호인 22번을 열어줌
* ssh_config : 내부 서버에서 외부 서버에 접속하기 위한 설정
* sshd_config : 외부 서버에서 내부 서버에 접속하기 위한 설정
* /etc/ssh에 있는 sshd_config파일 수정   
![ssh2](https://user-images.githubusercontent.com/57285121/115656016-62402380-a36f-11eb-9ca1-fd9e271ac4d3.PNG)
* Port 22의 주석을 해제   
![ssh3](https://user-images.githubusercontent.com/57285121/115656122-9582b280-a36f-11eb-815d-3963311673c4.PNG)
* SSH 서버 서비스 시작 : ```service sshd start```   
![ssh4](https://user-images.githubusercontent.com/57285121/115656344-0d50dd00-a370-11eb-94f3-19eb4d7ef16c.PNG)
* SSH 서버의 상태 확인 : ```service sshd status```   
![ssh5](https://user-images.githubusercontent.com/57285121/115656783-bbf51d80-a370-11eb-9cb7-23ab35f9048d.PNG)   
(active 상태 확인)

# SSH Client 설치 - PuTTY

* Windows에서 원격지에 접속하기 위한 프로그램 설치 - PuTTY
* PuTTY 설치 : [PuTTY](https://putty.softonic.kr, "PuTTY link")

# SSH Server에 접속하기 위한 사용자이름과 비밀번호 지정

* 사용자 추가 : ```useradd <사용자 이름>```
* 사용자 계정 비밀번호 설정 및 변경 : ```passwd <사용자 이름>```    
![ssh7](https://user-images.githubusercontent.com/57285121/115659835-1ba1f780-a376-11eb-800d-66156c9efe59.PNG)

# SSH Server 접속

* PuTTY 실행 후 원격지의 IP와 Port번호 입력
* 연결 타입에서 SSH 선택   
![ssh6](https://user-images.githubusercontent.com/57285121/115657618-29557e00-a372-11eb-8717-2780aeeb1edb.png)
* 서버에서 설정한 사용자 계정과 비밀번호로 접속   
![ssh8](https://user-images.githubusercontent.com/57285121/115660357-d92cea80-a376-11eb-9e5f-bc3ea5b40a46.PNG)   
* 접속 완료

