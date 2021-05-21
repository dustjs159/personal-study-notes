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
> * CentOS, RedHat : yum install openssh-server   
> * Ubuntu, Debian : apt-get install openssh-server   
* 잘 설치가 되었는지 확인 : which sshd   
![ssh1](https://user-images.githubusercontent.com/57285121/115655878-18efd400-a36f-11eb-83e6-821f19b2e900.PNG)

# SSH Server 작동

* SSH의 포트번호인 22번을 열어줌
* ssh_config : 내부 서버에서 외부 서버에 접속하기 위한 설정
* sshd_config : 외부 서버에서 내부 서버에 접속하기 위한 설정
* /etc/ssh에 있는 sshd_config파일 수정   
![ssh2](https://user-images.githubusercontent.com/57285121/115656016-62402380-a36f-11eb-9ca1-fd9e271ac4d3.PNG)
* Port 22의 주석을 해제   
![ssh3](https://user-images.githubusercontent.com/57285121/115656122-9582b280-a36f-11eb-815d-3963311673c4.PNG)
* SSH 서버 서비스 시작 : service sshd start   
![ssh4](https://user-images.githubusercontent.com/57285121/115656344-0d50dd00-a370-11eb-94f3-19eb4d7ef16c.PNG)
* SSH 서버의 상태 확인 : service sshd status   
![ssh5](https://user-images.githubusercontent.com/57285121/115656783-bbf51d80-a370-11eb-9cb7-23ab35f9048d.PNG)   
(active 상태 확인)

# SSH Client 설치 - PuTTY

* Windows에서 원격지에 접속하기 위한 프로그램 설치 - PuTTY
* PuTTY 설치 : [PuTTY](https://putty.softonic.kr, "PuTTY link")

# SSH Server에 접속하기 위한 사용자이름과 비밀번호 지정

* 사용자 추가 : useradd <사용자 이름>
* 사용자 계정 비밀번호 설정 및 변경 : passwd <사용자 이름>    
![ssh7](https://user-images.githubusercontent.com/57285121/115659835-1ba1f780-a376-11eb-800d-66156c9efe59.PNG)

# SSH Server 접속

* PuTTY 실행 후 원격지의 IP와 Port번호 입력
* 연결 타입에서 SSH 선택   
![ssh6](https://user-images.githubusercontent.com/57285121/115657618-29557e00-a372-11eb-8717-2780aeeb1edb.png)
* 서버에서 설정한 사용자 계정과 비밀번호로 접속   
![ssh8](https://user-images.githubusercontent.com/57285121/115660357-d92cea80-a376-11eb-9e5f-bc3ea5b40a46.PNG)   
* 접속 완료

# SSH Key를 이용하여 로그인 없이 접속
* 비밀번호보다 높은 수준의 보안으로 접속
* 로그인 없이 자동으로 서버에 접속
<img width="551" alt="스크린샷 2021-05-14 오후 9 58 00" src="https://user-images.githubusercontent.com/57285121/118273901-7525be00-b4ff-11eb-833f-3eb13df8ad2b.png">   

* 키를 생성하면 Public Key와 Private Key가 만들어 짐
* Public Key는 클라이언트(로컬)에, Private Key는 서버(원격지)에 위치해야 함
* 호스트가 원격지에 SSH 접속을 시도하면 호스트가 가지고 있는 Private Key와 원격지의 Public Key를 비교하여 일치하면 인증이 성공

* **ssh-keygen** 명령어로 키 생성(default : RSA)
<img width="707" alt="스크린샷 2021-05-14 오후 10 14 29" src="https://user-images.githubusercontent.com/57285121/118275738-c636b180-b501-11eb-8569-6a5b79e86827.png">   

<img width="506" alt="스크린샷 2021-05-14 오후 10 17 35" src="https://user-images.githubusercontent.com/57285121/118276082-32191a00-b502-11eb-849e-d47ef6fec727.png">   

id_rsa : 클라이언트의 Private Key / id_rsa.pub : 원격지의 Public Key   

id_rsa와 id_rsa.pub을 비교하여 인증을 진행   

클라이언트 측에서 scp명령어를 이용하여 원격지에 id_rsa.pub파일을 전송
scp <전송할 파일의 경로> <전송받을 계정명>@<IP 주소>:<전송받을 경로>
<img width="700" alt="스크린샷 2021-05-14 오후 11 25 43" src="https://user-images.githubusercontent.com/57285121/118284747-b754fc80-b50b-11eb-8158-960c1ecea521.png">

<img width="561" alt="스크린샷 2021-05-14 오후 11 01 00" src="https://user-images.githubusercontent.com/57285121/118281520-419b6180-b508-11eb-828b-16d01d8b7f74.png">
id_rsa.pub 수신 성공

서버측에 id_rsa.pub를 보관할 .ssh 디렉토리를 만들어 줌(권한은 소유자 외 접근 금지 : chmod 700)
(중요한 키를 보관하는 디렉토리라서)
<img width="474" alt="스크린샷 2021-05-14 오후 11 06 54" src="https://user-images.githubusercontent.com/57285121/118282270-15341500-b509-11eb-94bf-dc6c5d742881.png">

cp 명령어를 이용해서 home 디렉토리의 id_rsa.pub을 .ssh디렉토리 아래에 authorized_keys라는 이름으로 저장(home 디렉토리의 id_rsa.pub는 그대로)
<img width="542" alt="스크린샷 2021-05-14 오후 11 36 27" src="https://user-images.githubusercontent.com/57285121/118286235-36970000-b50d-11eb-877f-38b08dcc02e8.png">   

ssh <계정명>@<IP주소> 명령어를 통해 원격지에 접속   
<img width="636" alt="스크린샷 2021-05-14 오후 11 37 47" src="https://user-images.githubusercontent.com/57285121/118286424-6514db00-b50d-11eb-8efc-6292322ecdd5.png">   
비밀번호를 통한 로그인이 아닌 키 인증으로 로그인 성공

## SSH Key 통합 관리
* 원격지 서버의 .ssh 디렉토리에 config파일 추가
