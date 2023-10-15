Linux Ulimit
====================================
## Summary
- Last Updated : 21.09.02 Thu   
- Updated by : 윤연선
-----------------------------------

# ulimit
* 서버를 구축할 경우에 사용자가 늘어나게 되면 자연스레 처리해야할 요청이 많아지게 되는데 이 때 프로세스가 자원 사용에 제한이 생긴다면 늘어나는 요청을 더 이상 처리를 하지 못하게 됩니다.
* `ulimit` 명령어는 프로세스들의 자원 사용 한도(limit)를 확인하고 설정하는 명령어입니다. 자원 사용 한도는 soft, hard 두 가지의 종류가 있습니다.
* soft 한도 : 프로세스 실행 시 기본으로 적용되는 한도(default)
* hard 한도 : soft 한도에서 최대로 늘릴 수 있는 한도. root 사용자만이 값을 변경할 수 있습니다. 
* 영구 설정 파일 : /etc/security/limits.conf

# 명령어 및 옵션
* ``$ ulimit -a`` : 모든 자원 사용 한도를 출력(soft 한도)
* ``$ ulimit -aH`` : hard 한도 설정 확인

# ulimit 설정값 확인
   
<img width="427" alt="스크린샷 2021-08-06 오후 5 48 36" src="https://user-images.githubusercontent.com/57285121/128484016-80861a46-60ce-40ea-95e7-e8ee75b3fd49.png">
   
* core file size : core dump 파일(프로그램이 비정상적으로 종료되는 경우 그 당시의 상태를 기록하여 생성한 파일. 주로 디버깅 목적으로 사용)의 개수 제한. 0이면 core dump파일이 생성되지 않음
* data seg size : 메모리 영역중 힙 영역에 할당할 수 있는 메모리의 크기 제한
* scheduling priority : 프로세스의 우선순위(nice 값. nice값은 default가 0이며 -20 ~ 19까지 순위 값을 조정할 수 있고 숫자가 작을 수록 우선 순위가 높음)
* **file size** : shell에서 생성할 수 있는 파일의 최대 크기
* pending signals : 특정 event의 발생으로 인한 신호가 프로세스에게 바로 전달되지 않고 대기할 수 있는 한계
* max locked memory : 메모리에 적재될 수 있는 잠금 파일의 최대 크기
* max memory size :  메모리에 적재되는 프로세스의 최대 크기 제한
* **open files** : 프로세스가 open 할 수 있는 **File Descriptor**의 제한
* pipe size : 파이프 파일 크기 
* real-tiem priority : RT(Real Time) 프로세스들의 우선순위. RT 프로세스들은 일반 프로세스보다 우선순위가 높아야 함. (priority 값. priority 값의 범위는 1 ~ 139이고 낮은 숫자일 수록 우선 순위가 높음)
* stack size : 메모리 영역중 스택 영역에 할당할 수 있는 메모리의 크기 제한
* cpu time : 초단위로 사용 가능한 CPU의 사용 시간 제한
* **max user processes** : 하나의 user가 사용 가능한 프로세스의 최대 개수
* virtual memory : 가상 메모리의 최대 개수 제한
* file locks : 잠금 파일의 개수 제한

# File Descriptor
* Linux, UNIX 계열에서는 모든 객체들을 **파일**로 취급합니다. 파일의 종류는 일반 파일과 디렉토리 파일 이외에도 특수한 파일들이 존재합니다.
* File Descriptor는 프로세스가 파일에 접근하기 위한 **0이 아닌 정수** 
* 프로그램을 실행하여 프로세스가 메모리에 적재되면(= 파일을 오픈하면) 커널은 FD 테이블에서 사용하지 않는 FD(File Descriptor)중 가장 작은 FD를 할당. 이 때 0, 1, 2는 예약된 FD. (0은 표준 Input, 1은 표준 Output, 2는 표준 Error)
* 그 이후에는 프로세스가 파일들을 제어할 때(실행, 중지, 종료 등) 할당한 FD를 사용하여 제어(반복적으로 파일들을 제어하기 용이함)
* fd 확인 경로 :  /proc/[PID 번호]/fd 

## 파일(File)의 종류
   
|파일 종류|표기 문자|
|------|---|
|일반 파일|-|
|디렉토리 파일|d|
|링크 파일(Symbolic)|l|
|링크 파일(Hard)|원본 파일과 동일|
|장치 파일(Character)|c|
|장치 파일(Block)|b|
|파이프 파일(Pipe)|p|
|소켓 파일(Socket)|s|
   
* 일반 파일 : 가장 흔하게 볼 수 있는 텍스트 파일을 포함한 이미지 파일, 바이너리 파일, 스크립트 파일 등
* 디렉토리 파일 : 파일, 디렉토리를 저장할 수 있는 디렉토리.
* 링크 파일(Symbolic / Hard) : 파일의 복사본. Symbolic 링크는 원본 파일을 대신해 원본 파일로 바로가기를 만드는 링크이고 Hard 링크는 원본 파일과 똑같은 사본을 하나 더 만드는 링크.
* 장치파일(device)  
> * Character 장치 파일 : 키보드, 마우스 등 I/O 장치들. I/O 속도가 다소 느릴 수 있음   
> * Block 장치 파일 : 디스크(HDD, 플로피디스크 등의 저장장치). I/O 속도가 상대적으로 빠름   
* 파이프(Pipe) 파일 : 특정 프로세스의 출력 결과를 다른 프로세스의 입력으로 바로 보내는 역할. 프로세스 간 통신이 가능합니다.
* 소켓(Socket) 파일 : 네트워크를 통해 데이터 통신하기 위한 파일(API 사용).   


