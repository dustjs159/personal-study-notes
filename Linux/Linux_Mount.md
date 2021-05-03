Mount in Linux
=====================

# Mount ?
* 윈도우와 다르게 리눅스에서는 HDD의 파티션, CD/DVD, USB 등을 사용하려면 지정한 디렉토리의 위치에 연결해야함
* 물리적 장치를 특정 디렉토리에 연결시키는 과정
* 마운트 전, 하드 디스크를 추가하고 파티션하는 과정과 파일시스템을 입혀주는 포맷 과정이 필요

# 0. 디스크의 정보 확인
* df : 현재 디스크 여유 공간 확인 (disk free)  
<img width="570" alt="스크린샷 2021-05-03 오후 12 13 20" src="https://user-images.githubusercontent.com/57285121/116838329-f54b4a00-ac08-11eb-94fb-7f928879773f.png">   

> * -T : 파일 시스템 타입 출력   
> * -h : 사람이 읽을 수 있는 단위의 용량으로 표시   

# 1. 디스크 파티션 나누기
* fdisk : 파티션 테이블을 관리하는 명령어    
> * 리눅스의 디스크 파티션을 생성, 수정, 삭제할 수 있는 유틸리티.   
> * fdisk -l : 디스크 파티션 리스트 출력   
<img width="653" alt="스크린샷 2021-04-30 오후 10 22 54" src="https://user-images.githubusercontent.com/57285121/116863344-2182bd00-ac41-11eb-93b6-31de074588d6.png">   
 
* fdisk <파티션을 나누지 않은 디스크 이름> : 해당 디스크를 파티션으로 나눔   
<img width="612" alt="스크린샷 2021-04-30 오후 10 23 24" src="https://user-images.githubusercontent.com/57285121/116865106-f51c7000-ac43-11eb-8082-e00a08eb1d71.png">   
 
> * Command : n (new)   
<img width="456" alt="스크린샷 2021-04-30 오후 10 24 09" src="https://user-images.githubusercontent.com/57285121/116865276-4af11800-ac44-11eb-815c-8618b0613674.png">   

> * Pratition type : p (주 파티션, Primary Partition)   
<img width="462" alt="스크린샷 2021-04-30 오후 10 24 36" src="https://user-images.githubusercontent.com/57285121/116865935-86d8ad00-ac45-11eb-88d7-d2430db31259.png">   

> * Partition number : 1 (파티션 개수)   
> * First sector : 2048(default)   
> * Last sector : 41943039(default)   
> * Command : w (write)   
<img width="692" alt="스크린샷 2021-04-30 오후 10 25 40" src="https://user-images.githubusercontent.com/57285121/116866066-bab3d280-ac45-11eb-8294-4617d8287b63.png">   

<img width="693" alt="스크린샷 2021-04-30 오후 10 26 51" src="https://user-images.githubusercontent.com/57285121/116866691-d23f8b00-ac46-11eb-9d12-7a17c906b1f1.png">   


# 2. 포맷(파일 시스템 적용)
* mkfs : 디스크에 파일시스템을 입혀주는 포맷작업을 진행    
> * mkfs.<파일시스템명> <파티션을 나눈 디스크이름> : 해당 디스크에 파일 시스템을 적용하는 포맷 작업 진행   
<img width="690" alt="스크린샷 2021-04-30 오후 10 29 13" src="https://user-images.githubusercontent.com/57285121/116863950-0795aa00-ac42-11eb-851f-addd76681cef.png">   

<img width="609" alt="스크린샷 2021-04-30 오후 10 30 20" src="https://user-images.githubusercontent.com/57285121/116866883-0adf6480-ac47-11eb-83fe-f3ea1d00a126.png">   


# 3. 마운트
* mount : 디스크를 디렉토리에 마운트함   
> * mount <포맷완료된 디스크> <마운트할 디렉토리>   
<img width="597" alt="스크린샷 2021-05-03 오후 7 45 20" src="https://user-images.githubusercontent.com/57285121/116867420-1aab7880-ac48-11eb-91f6-13c2dbb74b89.png">   
* umount : 마운트 해제   
> * umount <디스크>   
<img width="553" alt="스크린샷 2021-05-03 오후 7 49 02" src="https://user-images.githubusercontent.com/57285121/116867763-9f969200-ac48-11eb-84f6-c04be69ae7e7.png">   

# 4. 영구적인 마운트
* 시스템 재부팅 시에도 마운트 상태 유지
* /etc/fstab파일 수정   
> * <디스크이름> <마운트 디렉토리 위치> <파일시스템명> <마운트옵션> <Dump(백업)필드> <File Sequence Check Option>   
<img width="412" alt="스크린샷 2021-05-03 오후 7 58 01" src="https://user-images.githubusercontent.com/57285121/116868518-e0db7180-ac49-11eb-92f5-72ae3c19a393.png">   
> * 마운트옵션   
|옵션|이름|   
|------|---|   
|auto|부팅 시 자동마운트|   
|exec|실행파일 실행 허용|   
|ro|읽기 전용으로 파일 시스템 설정|    
|rw|읽기/쓰기 전용으로 파일 시스템 설정|    
|user|일반 사용자 마운트 가능|   
|nouser|일반 사용자 마운트 불가능, root만 가능|   
|default|rw, nouser, auto, exec, suid속성을 모두설정|   
> * Dump(백업)필드   
> > * 0 : Dump 불가 / 1 : Dump 가능   

> * File Sequence Check Option : 무결성 검사 우선 순위   
> > * 0 : 무결성 검사 X   
> > * 1 : 우선순위 1위, root설정   
> > * 2 : root설정부분 검사 후 검사진행

