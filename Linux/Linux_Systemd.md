Linux Systemd 
====================================
## Summary
- Last Updated : 21.06.24 Thu   
- Updated by : 윤연선
-----------------------------------

# systemd
* 기존의 리눅스에서 가장 먼저 실행되는 init 프로세스를 대체하는 시스템
* **Unit**단위로 서비스(데몬)들을 관리하는 시스템 자원 통합 관리 매니저
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
* After : 현재 유닛이 실행된 후 실행되는 유닛들의 순서 목록
* Before : 현재 유닛이 실행되기 전 실행되어야 할 유닛들의 순서 목록
* Wants : 의존성 관련 옵션. 작성된 유닛들이 전부 실행되지 않더라도 현재 유닛 실행 가능
* Requires : 의존성 관련 옵션. 작성된 유닛들이 모두 실행되어야 현재 유닛이 실행됨

### [Unit 종류] 섹션
* 유닛의 유형을 정의
* Service, Target, Timer, Socket 등의 유닛 유형을 정의

### [Install] 섹션
* WantedBy
* RequiredBy

## Unit 종류
* Service Unit : 서비스 유닛. '서비스 유닛명.service'
* Target Unit : 시스템 부팅환경과 관련된 유닛. '타겟 유닛명.target'
* Timer Unit : 타이머 관련 유닛. '타이머 유닛명.timer'
* Socket Unit : 소켓 유닛. '소켓 유닛명.socket'

## systemd 구성
* coredump.conf
* journald.conf
* logind.conf
* resolved.conf
* system.conf
* user.conf
 
