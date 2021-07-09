Linux_Process 
====================================
## Summary
- Last Updated : 21.07.07 Wed   
- Updated by : 윤연선
-----------------------------------

# 프로세스(Process)
* 보조기억장치(하드디스크, SSD 등)에 저장된 프로그램이 주기억장치(RAM, ROM)에 적재되어 활성화 된 것
* 모든 프로세스들은 Foreground 혹은 Background 두가지 중 하나의 모드로 작동

## Foreground Process
* 실행 시 화면에 나타나서 사용자와 상호 작용하는 프로세스
* 화면에서 실행되는 것이 보이는 프로세스
* 대부분의 응용 프로그램

## Background Process
* 실행은 되었지만 화면에는 나타나지 않고 실행되는 프로세스
* 백신 프로그램, **서버 데몬** 등
* Background Process 확인 : ```jobs -l```

## 프로세스 번호(PID)
* 프로세스 식별자(PID : Process Identification Number)
* 메모리에 로딩되어 활성화된 프로세스를 구분하기 위한 각각의 고유 번호
* 프로그램 실행 시 메모리에 적재되며 OS에서 랜덤하게 번호 할당(실행할 때마다 바뀜)
* 메모리에서 활성화된 프로세스를 강제로 제거하기 위해 사용

## 작업 번호
* 현재 실행되고 있는 백그라운드 프로세스의 순차 번호

## 부모 프로세스 & 자식 프로세스
* 모든 프로세스는 부모 프로세스를 가지고 있음
* 부모 프로세스의 식별자는 PPID(Parent PID). Ex) 자식 프로세스의 PPID가 3103일 경우 해당 프로세스의 부모 프로세스의 PID가 3103.
* 부모 프로세스를 kill(종료)하면 자식 프로세스도 자동으로 kill
* 쉘에서 명령어를 입력해 프로그램 실행 시 쉘이 부모 프로세스가 되고 프로세스의 PPID가 쉘의 PID가 됨
* 리눅스에서 프로세스를 생성하는 가장 일반적인 방법 : fork() 
* fork()를 실행한 프로세스 -> 부모 프로세스
* fork()로 생성된 프로세스 -> 자식 프로세스
* 부모 프로세스는 자식 프로세스가 종료되기 전 까지 wait 상태가 되는데, 만약 부모 프로세스가 자식 프로세스보다 먼저 종료될 시에 자식 프로세스는 부모 프로세스를 잃게되어 좀비 프로세스가 됨

## 주요 명령어
### ps
* Process Status
* 현재 프로세스의 상태 확인
* 주로 ``ps -ef | grep <프로세스 이름>`` 형식으로 많이 사용
   
<img width="721" alt="스크린샷 2021-06-15 오전 3 38 02" src="https://user-images.githubusercontent.com/57285121/121942118-17e58c80-cd8b-11eb-8918-4ab5b8e5b77a.png">
   
* 구성   
> * UID : 프로세스의 실행 / 소유자 ID   
> * PID : 프로세스 ID   
> * PPID : 부모 프로세스 ID   
> * C : 프로세스 우선순위(높을수록 우선순위)   
> * STIME : 프로세스의 시작 시간   
> * TTY : 프로세스가 수행되고 있는 터미널을 표시('?' : 터미널에 연결되어 있지 않음)   
> * TIME : 프로세스 실행 시간    
> * CMD : 프로세스를 실행할 당시 커맨드 라인   

### kill
* 프로세스 강제종료
* ```kill -9 <PID Number>```
   
<img width="921" alt="스크린샷 2021-06-16 오전 12 38 36" src="https://user-images.githubusercontent.com/57285121/122082721-30ad7b00-ce3b-11eb-9777-413249b37c89.png">
   
### pstree
* 부모 프로세스와 자식 프로세스의 관계를 트리 형태로 보여줌
* 주로 ```pstree -p``` 형식으로 PID 번호까지 확인하여 사용
   
<img width="551" alt="스크린샷 2021-06-16 오전 1 30 36" src="https://user-images.githubusercontent.com/57285121/122090184-7588e000-ce42-11eb-8614-236f53dbbcca.png">
   
## Foreground / Background Process Test
1. 30초 동안 동작을 멈추는 스크립트 작성 `test`
   
<img width="112" alt="스크린샷 2021-06-16 오전 1 53 33" src="https://user-images.githubusercontent.com/57285121/122093100-aa4a6680-ce45-11eb-9616-b96f7db9e038.png">
   
2. 스크립트 실행 : ```bash test```

3. ```control + z``` 로 프로세스 일시 정지(프로세스 종료는 ```control + c```)

4. ```jobs -l```와 ```ps -ef | grep test```로 정지된 백그라운드 프로세스 확인
   
<img width="672" alt="스크린샷 2021-06-16 오전 2 26 00" src="https://user-images.githubusercontent.com/57285121/122097051-32cb0600-ce4a-11eb-835e-e37bfa92a874.png">
   
5. ```bg <작업번호>```로 프로세스를 백그라운드에서 실행 후 30초 중 남은 시간이 지나면 프로세스 동작 종료

6. 다시 ```ps -ef | grep test```로 종료된 프로세스 확인
   
<img width="676" alt="스크린샷 2021-06-16 오전 2 29 10" src="https://user-images.githubusercontent.com/57285121/122097438-a40ab900-ce4a-11eb-87f2-dd97302b3c72.png">
   
### 처음부터 Background Process로 실행
* 스크립트 실행 시 끝에 `&`를 붙여줌
   
<img width="429" alt="스크린샷 2021-06-16 오전 2 31 28" src="https://user-images.githubusercontent.com/57285121/122097724-f64bda00-ce4a-11eb-933e-422d76ba0b29.png">
   
### Background Process를 Foreground로 실행
* ``fg <작업번호>``
   
<img width="317" alt="스크린샷 2021-06-16 오전 2 32 59" src="https://user-images.githubusercontent.com/57285121/122097919-2d21f000-ce4b-11eb-9c65-742e10eec097.png">
   
## top
* 실시간 CPU 점유율 확인
   
<img width="972" alt="스크린샷 2021-06-03 오후 12 59 19" src="https://user-images.githubusercontent.com/57285121/120584843-a85acd80-c46b-11eb-9cf0-ed1f47c0265a.png">
   
* 구성(CPU & 메모리)   
> * top : 서버 시간, 접속자 수, 부하율(load average)   
> * Tasks : 가동중인 프로세스, 대기중인 프로세스   
> * %Cpu(s) : 사용자(us) / 시스템(sy) 레벨 사용 CPU 비중, 유휴 상태(id)의 CPU 비중   
> * Mem : 전체 메모리(total), 남아있는 여유메모리(free), 사용중인 메모리(used)   
> * Swap : 전체 스왑 메모리(total), 남아있는 여유 스왑 메모리(free), 사용중인 스왑 메모리(used)   
* 구성(프로세스 상태)   
> * PID : 프로세스 ID   
> * USER : 프로세스를 실행시킨 사용자 ID   
> * PRI : 프로세스 우선 순위(낮을 수록 높음)   
> * NI : nice value.(마이너스를 가질수록 우선순위가 높음)   
> * VIRT : 가상 메모리 사용량(Swap+RES)   
> * RES : 현재 페이지가 상주하고 있는 크기(Resident Size)   
> * SHR : 프로세스에 의해 사용된 메모리를 나눈 메모리의 총합   
> * S(Sleeping), R(Running)   
> * %CPU, %MEM : 프로세스가 사용하는 CPU사용률, 메모리 사용률   

