CentOS
====================================
## Summary
- Last Updated : 21.06.02 Wed    
- Updated by : 윤연선
-----------------------------------

# CentOS ?

# CentOS 6 Vs CentOS 7
## service & systemctl
* CentOS 6이전 : /etc/rc.d/init.d디렉토리에 서비스 관리 스크립트가 존재하고, 스크립트를 통해 서비스 관리
* CentOS 7 : 스크립트들이 서비스 유닛으로 변경. /etc/systemd에서 서비스 관리
   
|기능|CentOS 6|CentOS 7|
|------|---|---|
|서비스 상태|service 서비스명 status|systemctl status 서비스명|
|서비스 시작|service 서비스명 start|systemctl start 서비스명|
|서비스 정지|service 서비스명 stop|systemctl stop 서비스명|
|서비스 재시작|service 서비스명 restart|systemctl restart 서비스명|
|서비스 리로드|service 서비스명 reload|systemctl reload 서비스명|
   

## chkconfig & systemctl
   
|기능|CentOS 6|CentOS 7|
|------|---|---|
|자동시작 확인|chkconfig 서비스명|systemctl is-enabled 서비스명|
|자동시작 설정|chkconfig 서비스명 on|systemctl enable 서비스명|
|자동시작 해제|chkconfig 서비스명 off|systemctl disable 서비스명|


* 부팅되는 과정에서 시스템을 초기화하고 기타 서비스들을 위한 환경을 만들고 시작시켜주는 일을 하는 초기화 프로세스가 필요함
* CentOS 6은 Sys V라고 해서 init프로세스가 이것을 담당(커널이 메모리에 올라가면 가장 먼저 init프로세스를 실행)
* CentOS 7은 Sys V의 init프로세스를 버리고 systemd로 대체. 
* init은 부팅시 순차적 처리 / systemd은 부팅시 병렬 처리 (부팅속도 향상)

## xfs 파일시스템 지원
* 기존 ext4 보다 최대 볼륨 크기가 커지고 처리 가능한 단일 파일의 크기가 증가한 파일 시스템 xfs 지원


# CentOS 7 vs CentOS 8

## iptables / nftables





