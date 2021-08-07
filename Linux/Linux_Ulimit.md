Linux Ulimit
====================================
## Summary
- Last Updated : 21.08.06 Fri   
- Updated by : 윤연선
-----------------------------------

# Ulimit
* 각각의 사용자마다 실행한 프로세스들의 자원 사용 한도(Limit)를 설정
* 자원 한도는 soft / hard 로 분류 (soft가 default값)
* soft / hard 한도의 범위는 0 <= soft <= hard
* hard 한도는 root 사용자만이 값을 변경할 수 있습니다.
* 설정 파일 : /etc/security/limits.conf

# 주요 명령어
* ``$ ulimit -a`` : soft 한도 설정 확인
* ``$ ulimit -aH`` : hard 한도 설정 확인

# ulimit 설정값 확인
   
<img width="427" alt="스크린샷 2021-08-06 오후 5 48 36" src="https://user-images.githubusercontent.com/57285121/128484016-80861a46-60ce-40ea-95e7-e8ee75b3fd49.png">
   
> * core file : 코어 파일(프로세스가 비정상적으로 종료되었을 때의 상태를 기록하는 core dump 파일)의 최대 크기   
> * file size : shell에 의해 만들어질 수 있는 파일의 최대 크기 제한   
> * pending signals : 프로세스 간 발생하는 event들을 알리기 위한 신호   
> * max memory size : RAM에 상주할 수 있는 크기   
> * open files : 오픈할 수 있는 file descriptor의 한도   
> * pip size : 파이프 크기 설정(512 byte 단위)   
> * max user processes : 사용자 한명이 실행할 수 있는 프로세스의 최대 개수   

# File Discriptor
* 리눅스, 유닉스 계열에서는 모든 프로세스들이 **파일 단위**로 실행(shell에서 실행하는 명령어도 바이너리 형태의 파일)
* 프로세스를 실행하면(= 파일을 오픈하면) 커널은 사용하지 않는 FD(File Descriptor)중 가장 작은 FD를 할당하고 이후에는 이 FD 번호를 사용(0, 1, 2는 예약)
* /proc/[pid]/fd에서 확인 가능
   
<img width="656" alt="스크린샷 2021-08-07 오후 1 30 46" src="https://user-images.githubusercontent.com/57285121/128587910-f57eb7e4-da6d-4565-822d-8f4064aa4aa9.png">
   
> * 0 : 표준 입력   
> * 1 : 표준 출력   
> * 2 : 표준 에러

