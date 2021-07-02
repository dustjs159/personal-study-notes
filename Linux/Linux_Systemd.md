Linux Systemd 
====================================
## Summary
- Last Updated : 21.07.01 Thu   
- Updated by : 윤연선
-----------------------------------

# systemd
* 기존의 리눅스에서 가장 먼저 실행되는 init 프로세스를 대체하는 시스템
* **Unit**단위로 서비스(데몬)들을 관리하는 프로세스 자원 통합 관리 매니저
* 모든 프로세스들의 부모 프로세스가 됨
* /etc/systemd에 위치
* **PID = 1**

# systemd Unit
* /etc/systemd/system : 시스템 관리자가 수동으로 생성 및 관리하는 유닛들이 저장되는 디렉토리. 부팅시 사용
* /usr/lib/systemd/system : 유닛을 포함한 패키지 설치 시 유닛들이 저장되는 디렉토리. 유닛들의 스크립트 실행 파일이 위치

## Unit Configuration File

### [Unit] 섹션
* 유닛에 대한 일반적인 정보들을 작성
* Description : 유닛의 이름과 간단한 설명. systemd가 구별할 수 있어야 함
* Documentation : 유닛의 구성과 관련이 있는 문서표시
* After : 현재 유닛이 **실행되기 전 실행되어야 할 유닛**들의 순서 목록(낚시 주의)
* Before : 현재 유닛이**실행된 후 실행할 유닛**들의 순서 목록(헷갈림 주의)
* Wants : 의존성 관련 옵션. 작성된 유닛들이 전부 실행되지 않더라도 현재 유닛 실행 가능
* Requires : 의존성 관련 옵션. 작성된 유닛들이 모두 실행되어야 현재 유닛이 실행됨

### [Unit 종류] 섹션
* 유닛의 유형을 정의
* Service, Target, Timer, Socket 등의 유닛 유형을 정의

### [Install] 섹션
* WantedBy
* RequiredBy

# Unit 종류

## Service Unit
   
<img width="630" alt="스크린샷 2021-06-29 오전 2 54 33" src="https://user-images.githubusercontent.com/57285121/123681929-5ac45b80-d885-11eb-811f-b0be3d8cc4cf.png">
   
* 서비스 유닛. 'Service 유닛명.service'

### Service Unit의 Service 섹션
* Type : 유닛이 시작되는 유형 선언. ExecStart에 영향을 줌   
> * simple(default) : systemd가 실행될 때 ExecStart가 메인 프로세스가 됨   
> * notify : simple과 비슷. 유닛 작동 시 systmed에 시그널 전송 후 작동   
> * forking : 해당 유닛의 자식 프로세스까지 생성이 완료 되어야 systemd가 유닛이 작동되었다고 인식   
> * dbus : DBUS 준비 완료 이후에 유닛 작동   
* **EnvironmentFile** : 서비스 유닛의 환경 설정 파일(config)의 경로
* ExecStartPre : ExecStart 전에 실행할 명령어나 유닛의 절대경로
* **ExecStart** : 실행할 명령어나 유닛의 스크립트가 위치한 절대경로. ``$ systemctl start <서비스명>``
* ExecStartPost : ExecStart 후에 실행할 명령어나 유닛의 절대경로
* ExecStop : 유닛이 중지될 때 필요한 명령어나 스크립트의 절대경로. ``$ systemctl stop <서비스명>``
* ExecReload : 리로드를 위한 명령어나 스크립트의 절대경로.``$ systemctl reload <서비스명>``
* KillMode : 유닛의 프로세스가 어떻게 중지되는지 결정(KillMode=process는 메인 프로세스만 중지)
* Restart   
> * on-failure : 유닛의 종료상태가 0이 아닌 경우(exit!=0, 성공적인 종료상태가 아닐 경우) 유닛 재시작   
> * on-success : 유닛의 종료상태가 0인 경우(exit==0, 성공적인 종료 상태일 경우) 유닛 재시작   
* RestartSec : 서비스 재시작 전 sleep 상태 두는 시간

## Target Unit
* 시스템 부팅환경과 관련된 유닛. 'Target 유닛명.target'

### Target Unit의 Target 섹션 

## Timer Unit
* 타이머 관련 유닛. 'Timer 유닛명.timer'
* 일정 시간 지난 이후에 작업을 수행
* 기존 리눅스의 cron 프로세스가 systemd의 timer 유닛으로 넘어오게 됨

### Timer Unit의 Timer 섹션
* OnCalendar : realtimer 옵션. 지정한 날짜와 시간 및 요일마다 작업 수행   
> * `["요일"] "Year"-"Month"-"Day" "Hour":"Min":"Sec" [Timezone"]`   
> * 요일, Timezone은 생략 가능(Timezone 생략 시 시스템의 설정된 Timezone이 적용)   
> * 요일 : Mon/Tus/Wed/Thu/Fri/Sat/Sun ( '..' 으로 범위 지정 가능. Mon..Fri : 월 ~ 금)   
* AccuracySec : 타이머를 작동하는 주기(default : 1분)

## Socket Unit
* 소켓 유닛. 'Socket 유닛명.socket'

### Socket Unit의 Socket 섹션
# 주요 명령어
## systemctl
   
|기능|명령어|
|------|---|
|유닛 상태 및 정보|systemctl status 유닛명|
|유닛 실행|systemctl start 유닛명|
|유닛 중지|systemctl stop 유닛명|
|유닛 재시작|systemctl restart 유닛명|
|유닛 리로드|systemctl reload 유닛명|
|부팅시 자동시작 설정|systemctl enable 유닛명|
|부팅시 자동시작 해제|systemctl disable 유닛명|
|실행 상태인 유닛들 확인|systemctl list-units|
|등록된 유닛들의 상태(활성화, 비활성화, static)|systemctl list-unit-files|

* restart : stop 후 start(유닛 중단 후 다시 시작)
* reload : config파일만 다시 불러옴
* 서비스 상태의 static은 활성화 및 비활성화가 불가능. 다른 유닛과 의존성을 갖고있음

## journalctl
* systemd-journald.service데몬이 systemd의 로그를 기록
* 부팅 시 발생하는 이벤트를 수집해서 바이너리 형태의 저널 데이터 저장
* 저널 데이터는 /run/log/journal에 위치.(읽을 수 없다..) 재부팅시 삭제
* /etc/systemd에 설정파일 journald.conf가 있음


