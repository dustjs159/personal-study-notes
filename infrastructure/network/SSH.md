💻 [Network] SSH
=================

# 💡 SSH(Secure Shell) 
* 안전한 서버 원격 접속을 위한 프로토콜
* 포트번호는 22번을 사용
* config 파일 위치
  * `/etc/ssh/sshd_config`
  * `/etc/ssh/ssh_config`
  * `sshd_config` 파일은 현재 시스템이 SSH 서버가 될 때(Inbound) 참조하는 설정 파일이며 `ssh_config` 파일은 현재 시스템이 SSH 클라이언트가 될 때(Outbound) 참조하는 설정 파일

## 📌 SSH 동작 원리
* 클라이언트 - 서버 모델로 동작
* 각각 SSH 클라이언트 및 데몬이 설치되어 있어야 함 - Port 22
* SSH Connection을 수립하는 과정(서버 인증 & 클라이언트 인증)에서는 공개키 암호화 방식을 사용하며 Connection 수립 이후에는 대칭키 암호화 방식을 사용하여 데이터 통신
* 서버 인증 : 클라이언트는 접속하고자 하는 서버가 정상적인 서버인지 검증
  * **공개키 암호화 방식(Two Key)** 사용
* 클라이언트 인증 : 서버는 클라이언트가 서버에 접근할 수 있는지 검증
  * **공개키 암호화 방식(Two Key)** 사용
* 클라이언트와 서버가 성공적으로 검증 절차를 통과하게 되면 생성되는 세션 키를 통해 전송하는 데이터를 암호화하여 안전하게 전송
  * **대칭키 암호화 방식(One Key)** 사용
* passphrase 사용으로 보안 강화
  * Private Key를 저장할 때 passphrase로 한번 더 암호화 하여 저장
  * Private Key 분실을 대비하는 방법

## 📌 SSH Connection 수립 과정 
서버 인증 과정

![SSH Connection](https://user-images.githubusercontent.com/57285121/173183049-cdcd8396-6d4d-4db1-8746-741f895c9230.jpg)

1. 클라이언트가 서버(SSH 데몬이 실행중인)에 SSH Connection 요청. 이 때 각각 지원하는 암호화 방식을 서로 교환
2. 서버는 Public Key를 클라이언트에게 전달 
3. 클라이언트에게 서버로 부터 받은 Public Key를 받아 로컬에 저장할지 물어보고 이 때 `Yes`를 선택하면 `~/.ssh/known_hosts` 에 서버의 Public Key가 저장 됨
4. 클라이언트는 내부적으로 난수 값(Hash)을 생성, 난수 값을 서버의 Public Key로 암호화하여 서버에게 전송
5. 서버는 클라이언트로부터 받은 난수 값을 서버의 Private Key로 복호화.
6. 서버는 난수 값을 클라이언트에 전달, 복호화한 난수 값이 클라이언트의 난수 값과 일치하는지 검증. 검증 성공시 서버 인증 성공.

클라이언트 인증 과정

![SSH Connection (1)](https://user-images.githubusercontent.com/57285121/173183138-6cc80f48-4e4a-45e2-8fd9-5d4880365c77.jpg)

1. 클라이언트가 서버에게 SSH Connection 요청(Public Key 정보 전달)
2. 서버는 `~/.ssh/authorized_keys` 파일에 요청 받은 클라이언트의 Public Key 정보가 있는지 확인
3. `~/.ssh/authorized_keys` 파일에 클라이언트의 Public Key 정보가 등록되어 있다면 해당 Public Key로 서버 내부의 난수 값을 생성 및 암호화하여 클라이언트에게 전달
4. 클라이언트는 서버로부터 받은 난수 값을 클라이언트의 Private Key로 복호화.
5. 클라이언트는 난수 값을 서버에 전달, 복호화한 난수 값이 서버의 난수 값과 일치하는지 검증. 검증 성공시 클라이언트 인증 성공.

* 서버 및 클라이언트가 성공적으로 인증을 마친 후에는 SSH Connection이 수립되고 Session Key를 생성하여 데이터 통신 시 Session Key로 암호화하여 통신하게 됨
* SSH Connection이 종료된 후에는 내부적으로 Session Key를 폐기처리함

## 📌 sshd_config 파일 주요 옵션
* `PermitRootLogin`
  * `root` 계정으로 SSH 접속을 허용하는지 여부
  * `root` 계정 접속을 막는 것을 권고 ( `PermitRootLogin : no` )

## 📌 SSH Key 생성 명령어
* `ssh-keygen`
* 생성 시 별도의 경로를 지정하지 않으면 `~/.ssh` 경로에 `id_rsa.pub` (Public Key) 파일과 `id_rsa` (Private Key) 파일이 생성됨
* passphrase 입력은 필수 아님
* 옵션
  * `-t(type)` : 키 생성시에 사용할 알고리즘 타입
    * `# ssh-keygen -t rsa`
  * `-b(bit)` : 생성할 키의 크기
    * `# ssh-keygen -t rsa -b 2048`
  * `-f(file)` : 생성할 키 파일의 이름 지정
    * `# ssh-keygen -t rsa -b 4096 -f dev-key`

