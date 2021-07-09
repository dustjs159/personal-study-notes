Linux Systemd 
====================================
## Summary
- Last Updated : 21.07.06 Tue   
- Updated by : 윤연선
-----------------------------------

# systemd
* 과거의 리눅스에서는 부팅 시 가장 먼저 init 프로세스를 실행(즉 init 프로세스의 PID가 1)
* 그러나 최근의 리눅스에서 PID를 확인하면 systmed라는 프로세스의 PID가 1번에 위치하고 있는 것을 확인할 수 있음
   
<img width="692" alt="스크린샷 2021-07-06 오전 3 02 20" src="https://user-images.githubusercontent.com/57285121/124506428-966fa000-de06-11eb-934a-e0789b880519.png"> 
   
> * ``$ ps -ef``로 가동중인 프로세스들의 목록을 확인해본 결과 PID가 1인 프로세스가 systemd인 것을 확인   
* **Unit**단위로 서비스(데몬)들을 관리하는 프로세스 자원 통합 관리 매니저
* 모든 프로세스들의 부모 프로세스가 됨
* /etc/systemd에 위치
* **PID = 1** 

# systemd의 주요 구성
* systemd : init 데몬
* systemd-journald : 다른 데몬들의 로그 저장데몬
* systmed-logind : 사용자 로그인 관리 데몬
* systmed-udevd : 장치 관리자 데몬
* systmed-networkd : 네트워크 관리 데몬
* systmed-resolved : DNS 해석 데몬

# systemd Unit
* /etc/systemd/system : 시스템 관리자가 수동으로 생성 및 관리하는 유닛들이 저장되는 디렉토리. 부팅시 사용
* /usr/lib/systemd/system : 유닛을 포함한 패키지 설치 시 유닛들이 저장되는 디렉토리. 유닛들의 스크립트 실행 파일이 위치

## Unit의 종류와 구성 
* 유닛들의 구성은 스크립트 형식으로 [Unit], [Unit Type], [Install] 섹션으로 구성됨
* 유닛의 Type에 따라 Service, Target, Timer, Socket 등이 존재
   
|Unit|형식|기능|
|------|---|---|
|Service Unit|<Service 유닛명>.service|사용자 혹은 시스템에게 서비스 제공|
|Target Unit|<Target 유닛명>.target|시스템 부팅 관련|
|Timer Unit|<Timer 유닛명>.timer|반복 작업을 위한 유닛|
|Socket Unit|<Socket 유닛명>.socket|서로 다른 서비스간 데이터 통신시 사용|
   
### Service Unit
   
<img width="630" alt="스크린샷 2021-06-29 오전 2 54 33" src="https://user-images.githubusercontent.com/57285121/123681929-5ac45b80-d885-11eb-811f-b0be3d8cc4cf.png">
   
> * 예시 : sshd.service 유닛

#### [Unit] 섹션
* 유닛에 대한 일반적인 정보들을 작성
* Description : 유닛의 이름과 간단한 설명. systemd가 구별할 수 있어야 함
* Documentation : 유닛의 구성과 관련이 있는 문서표시
* After : 현재 유닛이 **실행되기 전 실행되어야 할 유닛**들의 순서 목록(낚시 주의)
* Before : 현재 유닛이**실행된 후 실행할 유닛**들의 순서 목록(헷갈림 주의)
* Wants : 의존성 관련 옵션. 작성된 유닛들이 전부 실행되지 않더라도 현재 유닛 실행 가능
* Requires : 의존성 관련 옵션. 작성된 유닛들이 모두 실행되어야 현재 유닛이 실행됨
* Conflicts : 역관계. 현재 유닛이 실행되면 Conflicts의 유닛들은 중지가되고 현재 유닛이 중지되면 Conflicts의 유닛이 실행

#### [Service] 섹션
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

#### [Install] 섹션
* WantedBy
* RequiredBy

### Target Unit

<img width="433" alt="스크린샷 2021-07-06 오전 3 41 36" src="https://user-images.githubusercontent.com/57285121/124509018-12b8b200-de0c-11eb-9f2f-079fc9ef7215.png">
   
> * 예시 : multi-user.target 유닛
   
* Target이란 과거의 리눅스에서 사용하던 init 프로세스의 runlevel 개념
   
|init|target|설명|
|----|----|------|
|runlevel 0|poweroff.target|시스템 종료|
|runlevel 1|rescue.target|single-user 모드|
|runlevel 2|multi-user.target|multi-user 모드(미사용)|
|runlevel 3|multi-user.target|multi-user 모드|
|runlevel 4|multi-user.target|multi-user 모드(미사용)|
|runlevel 5|graphical.target|multi-user + graphic mode(GUI)|
|runlevel 6|reboot.target|시스템 재부팅|
   
* Target 유닛은 별도의 Target 섹션이 없음

#### [Unit] 섹션
* 

### Timer Unit
* 일정 시간 지난 이후에 작업을 수행
* 기존 리눅스의 cron 프로세스가 systemd의 timer 유닛으로 넘어오게 됨

#### [Timer] 섹션
* OnCalendar : realtimer 옵션. 지정한 날짜와 시간 및 요일마다 작업 수행   
> * `["요일"] "Year"-"Month"-"Day" "Hour":"Min":"Sec" [Timezone"]`   
> * 요일, Timezone은 생략 가능(Timezone 생략 시 시스템의 설정된 Timezone이 적용)   
> * 요일 : Mon/Tus/Wed/Thu/Fri/Sat/Sun ( '..' 으로 범위 지정 가능. Mon..Fri : 월 ~ 금)   
* AccuracySec : 타이머를 작동하는 주기(default : 1분)
* Unit : 일정한 시간마다 실행시킬 서비스 혹은 스크립트 지정

#### Socket Unit
   
<img width="401" alt="스크린샷 2021-07-06 오전 3 54 58" src="https://user-images.githubusercontent.com/57285121/124510014-f0c02f00-de0d-11eb-8647-4ef25338db14.png">
   
> * 예시 : sshd.socket 유닛   

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


