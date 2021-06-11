CentOS
====================================
## Summary
- Last Updated : 21.06.11 Fri    
- Updated by : 윤연선
-----------------------------------

# CentOS ?

# CentOS 6 Vs CentOS 7
## service & systemctl
* CentOS 6이전 : /etc/rc.d/init.d 디렉토리에 서비스 관리 스크립트가 존재하고, 스크립트를 통해 서비스 관리
* CentOS 7 : 스크립트들이 서비스 유닛으로 변경. /etc/systemd에서 서비스 관리
* CentOS 7 이후 OS 들의 /etc/rc.d/init.d/README 파일을 확인
   
<img width="735" alt="스크린샷 2021-06-04 오전 12 22 55" src="https://user-images.githubusercontent.com/57285121/120670146-1bdff780-c4cb-11eb-9957-104e612fc0ee.png">
   
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
   
* service + chkconfig 명령어의 기능을 모두 포함하는 systemctl 명령어를 사용
* init은 부팅시 순차적 처리 / systemd은 부팅시 병렬 처리 (부팅속도 향상)

## xfs 파일시스템 지원
* 기존 ext4 보다 최대 볼륨 크기가 커지고 처리 가능한 단일 파일의 크기가 증가한 파일 시스템 xfs 지원

## iptables / firewalld
* firewalld : CentOS 7부터 채택된 **패킷 필터링**
* CentOS 6까지는 iptables에서 실행
* Linux 커널의 Netfilter의 동작(패킷 필터링)을 설정 및 관리
* iptables는 체인(INPUT, OUTPUT, FORWARD)마다 패킷 필터링을 적용
* firewalld는 zone(default : public)이라는 그룹 단위로 규칙을 정의
* iptables는 변경된 규칙을 적용하기 위해서는 서비스를 재시작해야함(서비스가 일시적으로 중단)
* firewalld는 임시 규칙, 지속적 규칙을 각각 관리할 수 있으며 서비스 재시작 없이 변경사항을 반영할 수 있음
* firewalld : **동적인 설정이 가능**
   
|기능|명령어|
|------|---|
|방화벽 실행 여부 확인|firewall-cmd --state|
|모든 zone의 정책 확인|firewall-cmd --list-all|
|정의된 서비스 목록 확인|firewall-cmd --get-services|
|허용된 서비스 목록 확인|firewall-cmd --list-services|
|변경 사항을 적용(리로드)|firewall-cmd --reload|
|영구적으로 서비스 등록|firewall-cmd --permanent --zone=<zone이름> --add-service=<서비스이름>|
|firewall-cmd --get-services|정의된 서비스 목록 확인|
|firewall-cmd --list -services|허용된 서비스 확인|
   
* /usr/lib/firewalld/services에 직접 xml파일을 만들어서 저장해서 서비스 사용 가능

# CentOS 7 vs CentOS 8

## dnf
* CentOS 8부터 기본적으로 설치 됨(/etc/dnf)
* 기존의 YUM보다 성능이 향상되어 YUM을 대체하게 됨 

## iptables / nftables
* iptables : 리눅스 환경에서 패킷을 제어하여 방화벽에대한 설정을 하는 도구(/etc/sysconfig)
* CentOS 8부터 nftables가 설치됨(/etc/nftables.conf)

## ntp / chrony
* CentOS 8부터 ntpd 지원이 종료되고 네트워크 시간 동기화 관련하여 chronyd가 사용됨(CentOS 7에서는 선택적으로 사용 가능)
* NTP는 /etc/npt에, chrony는 /etc/sysconfig에 위치
* NTP(network time protocol) : 네트워크 상 호스트들의 시간을 동기화 하는 프로토콜
* chronyd는 네트워크 혼잡시에도 성능이 상대적으로 우수

## Cockpit
* ntp보다 효율적인 메모리 사용

