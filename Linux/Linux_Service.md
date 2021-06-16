Service & Daemon 
====================================
## Summary
- Last Updated : 21.06.16 Wed   
- Updated by : 윤연선
-----------------------------------

# 서비스(Service)
* **데몬(Deamon) 이라고도 불리는 서버 프로세스**
* 서비스는 웹 서버, DB 서버 등의 서버 프로세스를 지칭(웹 서버 데몬, DB 서버 데몬이라고 부름)
* 주기억장치(메모리)에 상주하며 시스템과 독자적으로 구동되어 제공하는 프로세스
* CentOS 7 이전에는 /etc/rc.d/init.d의 init프로세스가 직접 서비스들을 관리 했었지만 CentOS 7 이후에는 /etc/systemd에서 관리
* /usr/lib/systemd/system : 서비스의 실행 스크립트 파일들이 위치. ```서비스이름.service```
* /etc/systemd : 서비스들을 관리하는 서비스 관리 매니저
* 서비스(데몬)는 시스템의 첫 프로세스인(PID가 1인)systemd의 바로 하위 프로세스. 때문에 PPID가 1이 됨

## 서비스와 데몬 차이
* 데몬도 서비스와 마찬가지로 **부팅 시 자동으로 켜지고 계속 백그라운드에서 실행되는 프로세스**
* 서비스 : 윈도우에서 사용
* 데몬 : 유닉스/리눅스에서 사용
* 리눅스에서는 데몬을 표현하기 위해 'd'를 붙이고 서비스를 표현하기 위해'service'를 붙임

## /etc/systemd
* 기존의 리눅스에서 가장 먼저 실행되는 init 프로세스를 대체하는 시스템. (PID = 1)
* 모든 프로세스들의 부모 프로세스가 됨
* 서비스(데몬)들을 관리하는 프로세스 관리 매니저

### journal
* systemd의 서비스 로그

## 주요 명령어
   
|기능|명령어|
|------|---|
|서비스 상태|systemctl status 서비스명|
|서비스 시작|systemctl start 서비스명|
|서비스 정지|systemctl stop 서비스명|
|서비스 재시작|systemctl restart 서비스명|
|서비스 리로드|systemctl reload 서비스명|
|자동시작 설정|systemctl enable 서비스명|
|자동시작 해제|systemctl disable 서비스명|

   
 


