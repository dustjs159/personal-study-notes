💻 [Network] SSH
=============

# 💡 SSH(Secure Shell) 
* 안전한 서버 원격 접속을 위한 프로토콜
* 포트번호는 22번을 사용
* config 파일 위치
  * `/etc/ssh/sshd_config`
  * `/etc/ssh/ssh_config`
  * `sshd_config` 파일은 현재 시스템이 SSH 서버가 될 때(Inbound) 참조하는 Config이며 `ssh_config` 파일은 현재 시스템이 SSH 클라이언트가 될 때(Outbound) 참조하는 Config


## 📌 동작 원리

<img width="551" alt="스크린샷 2021-05-14 오후 9 58 00" src="https://user-images.githubusercontent.com/57285121/118273901-7525be00-b4ff-11eb-833f-3eb13df8ad2b.png">

* SSH 서버는 외부로부터 SSH 접근 요청을 기다리는 sshd 데몬이 실행
* SSH 클라이언트가 `ssh-keygen` 으로 Public Key, Private Key를 생성
* 접속하고자 하는 SSH 서버의 `~/.ssh/authorized_keys` 파일에 클라이언트의 Public Key를 등록
* SSH 클라이언트가 접속 시도(인증 좀 해줘)
* SSH 서버는 `~/.ssh/authorized_keys` 에 등록된 Public Key를 클라이언트에게 전달(이거 복호화 해봐)
* 클라이언트는 Private Key로 전달 받은 Public Key를 복호화
* 인증 성공 시, 접속 허용

## 📌 sshd_config 파일 주요 옵션
* `PermitRootLogin`
  * `root` 계정으로 SSH 접속을 허용하는지 여부
  * `root` 계정 접속을 막는 것을 권고 ( `PermitRootLogin : no` )