RAID
====================================

# RAID(Redundant Array of Independent Disk)
* 복원을 위해 중복되는 데이터를 만들고 전체 데이터들을 나누어 각 독립적인 디스크들에게 배열하는 기술
* 두 개 이상의 디스크를 병렬로 처리하여 성능 및 안정성을 향상
* Disk를 여러 개 추가하여 하나인 것 처럼 사용

# RAID 종류
* Hardware RAID : 속도도 빠르고 안정적이지만 설치 비용이 비쌈
* Software RAID : 하드디스크만 있으면 구현 가능

# Linear RAID   
* 최소 두 개 이상의 하드디스크를 하나로 묶는 방식   
* 두 디스크가 각각 1GB 일 때 두 디스크를 묶어서 2GB인 것 처럼 사용
* 데이터를 디스크 하나에 먼저 저장 후 가득 차면 나머지 디스크에 저장
* 두 디스크중 먼저 저장되는 디스크가 고장이 났을 때 데이터 손실률이 매우 크다(신뢰성이 좋지 않은 방식)   
<img width="396" alt="스크린샷 2021-05-11 오전 11 48 40" src="https://user-images.githubusercontent.com/57285121/117750732-dd9a4400-b24e-11eb-8607-3f22cb76a617.png">   

# RAID 0
* 최소 두 개 이상의 하드디스크를 하나로 묶는 방식
* Striping
> * 데이터를 디스크에 하나씩 저장함 Ex) A - 1,3,5 / B - 2,4,6 ... 
> * 데이터를 동시에 저장하기 때문에 속도가 빠름
> * 두 디스크의 용량이 다르면 효율이 떨어짐 Ex) A : 2GB, B : 1GB 일 때 B가 가득 차면 A도 저장 못하게 됨
* Concatenate
> * Linear RAID와 유사한 방식   
> * 데이터를 순차적으로 저장하며 디스크 고장시 복구가 어려움

# RAID 1
* 디스크 두 개를 하나로 묶는 방식   
* 디스크를 두 개로 묶었지만 데이터를 저장할 수 있는 공간은 하나임
* Mirroring 방식
> * 두 디스크에 같은 데이터를 저장   
> * 저장할 수 있는 디스크는 사실상 하나밖에 없으므로 사용량이 절반으로 줄어들기 때문에 두 배의 저장공간이 필요하며 이에 따라 비용도 더 증가함   
> * 두 디스크중 하나가 고장나도 나머지 하나의 데이터가 보존됨(결함 허용)   
   
|구분|RAID 0|RAID 1|
|------|---|---|
|속도|빠름|상대적으로 느림|
|결함 허용|결함 허용 X|결함 허용 O|
|공간 효율|좋음|RAID 0에 비해 좋지 않음|   
   
# RAID 2
* Striping방식을 사용한 디스크와 오류 정정을 목적으로 해밍코드를 이용한 복구용 디스크를 묶어 구성하는 방식(RAID 0 - Striping + 복구용 디스크 - 해밍코드)   
* 복구용 디스크가 하나로 망가지면 사용 불가   
* 최근 디스크 드라이브가 기본적으로 에러검출 기능이 있기 때문에 거의 사용되지 않음

# RAID 3
* Striping방식을 사용한 디스크와 오류 검사를 위한 패리티 용도의 디스크를 묶어서 구성하는 방식(RAID 0 - Striping + 복구용 디스크 - 패리티)   
* 비트단위로 데이터를 저장

# RAID 4
* RAID 3과 동일한 방식으로 구성   
* RAID 3이 비트단위로 데이터를 저장했다면 RAID 4는 블록단위로 데이터를 저장   
* 비트보다 큰 단위인 블록단위로 데이터를 읽는다면 읽는 속도가 훨씬 빨라짐   

# RAID 5
* 최소 3개 이상의 디스크를 묶어서 사용하는 방식   
* RAID 0의 장점(공간 효율성) + RAID 1의 장점(데이터 안정성)   
* 3개 이상의 디스크 중 오류 발생시 복구를 위한 패리티를 위해 디스크 하나를 사용 Ex) A, B는 데이터 저장용, C는 데이터 복구를 위한 패리티)   
* 몇 개의 디스크를 묶든지 상관없이 패리티를 위한 디스크는 하나만 사용(공간 효율이 좋다)   
* 묶은 디스크 중 하나가 고장나도 데이터 사용이 가능하지만 디스크 두 개이상이 고장나면 데이터 사용 불가능(부분적 결함 허용)

# RAID 6
* 최소 4개 이상의 디스크를 묶어서 사용하는 방식   
* 4개 이상의 디스크 중 오류 발생시 복구를 위한 패리티를 위해 디스크 두 개를 사용 Ex) A, B는 데이터 저장용, C, D는 데이터 복구를 위한 패리티)   
* 몇 개의 디스크를 묶든지 상관없이 패리티를 위한 디스크는 두 개만 사용(공간 효율이 좋다)   
* 묶은 디스크 중 두 개가 고장나도 데이터 사용이 가능하지만 디스크 세 개이상이 고장나면 데이터 사용 불가능(RAID 5보다 강력한 결함 허용 제공)

|구분|RAID 5|RAID 6|
|------|---|---|
|속도|빠름|상대적으로 느림|
|신뢰성|RAID 6에 비해 좋지 않음|좋음|   
|최소 필요 디스크 개수|3개|4개|
|결함 허용 디스크 개수|1개(2개 이상 시 고장)|2개(3개 이상 시 고장)|   

# RAID 0+1 
* Striping방식으로 디스크 두 개를 묶은 다음 묶은 디스크를 Mirroirng방식으로 묶는 방법

# RAID 1+0
* Mirroring방식으로 디스크 두 개를 묶은 다음 묶은 디스크를 Striping방식으로 묶는 방법

#### RAID 0+1 / RAID 1+0 차이점
디스크 네 개(A, B, C, D)가 있다고 가정을 해 보자   

RAID 1+0 방식으로 디스크 ABCD를 묶었을 때 디스크 A에서 결함이 발생을 한다면 복구해야 할 디스크는 B를 통해서 A하나만 복구하면 된다.(Mirroring방식으로 A, B를 묶었기 때문)   
반면, RAID 0+1 방식으로 디스크 ABCD를 묶었을 때 디스크 A에서 결함이 발생한다면 복구해야할 디스크는 A,B 둘 다 복구를 해야한다. (Striping으로 A, B를 묶었기 때문)   
   
따라서 가격적인 면에서는 RAID 0+1이 더 저렴하긴 하지만 금융권같은 데이터가 중요시하게 다뤄지는 기관에서는 RAID 1+0을 많이 사용하고 있다.

# RAID 구현 실습
* RAID 구현 전 RAID로 묶을 하드디스크들을 추가
* 추가한 하드디스크들을 RAID용 파티션으로 만듦
1. fdisk -l 명령어로 디스크의 파티션 설정 현황 확인   
<img width="533" alt="스크린샷 2021-05-09 오후 2 46 49" src="https://user-images.githubusercontent.com/57285121/117752799-62d32800-b252-11eb-9af3-79c1b5d4fc74.png">   

2. 파티션이 생성되어있지 않기 때문에 fdisk <장치이름> 명령어로 하드디스크 파티션 생성 작업 진행   
<img width="698" alt="스크린샷 2021-05-09 오후 3 06 44" src="https://user-images.githubusercontent.com/57285121/117753099-decd7000-b252-11eb-920d-0b64fab6ec48.png">   

<img width="689" alt="스크린샷 2021-05-09 오후 3 06 26" src="https://user-images.githubusercontent.com/57285121/117753824-1852ab00-b254-11eb-8c9d-d7a71c3c99a9.png">   

> * Command : n		 	(새로운 파티션 분할)   
> * Selcet : p			(Primary 파티션 선택)   
> * Partition number : 1	(생성할 파티션 개수)   
> * First sector : Enter	(시작 섹터 번호)   
> * Last sector : Enter		(마지막 섹터 번호)   
> * Command : t			(파일 시스템 유형 선택)   
> * **Hex Code : fd		(Linux raid autodetect : RAID 구성에 이용되는 파일 시스템)**   
> * Command : w			(설정 저장)   

3. 파티션이 제대로 생성 되었는지 fdisk -l 명령어로 다시 확인   
<img width="626" alt="스크린샷 2021-05-11 오후 12 24 36" src="https://user-images.githubusercontent.com/57285121/117753684-de81a480-b253-11eb-818d-f6f1bbd08c17.png">   

4. **mdadm(Multiple Device ADMinistration) : 소프트웨어 RAID 장치를 생성/관리하는 명령어**   
> * --create <장치이름> : 	장치에 RAID 생성   
> * --level=<raid level> :  	raid level = linear, 0, 1 등등 RAID의 level   
> * --raid-devices=n <디스크이름1, 2 ... n> 	: RAID로 사용할 장치 개수와 이름   
> * --stop <RAID 장치이름>		: RAID 장치 중지   
> * --run <RAID 장치이름>		: 중지된 RAID 장치 다시 작동   
> * --detail <RAID 장치이름>		: 장치의 상세 내역 출력   
> * <RAID 장치이름> --add <디스크이름>	: 기존 RAID에 새 디스크를 추가함

## Linear RAID 구현   
<img width="878" alt="스크린샷 2021-05-09 오후 3 07 28" src="https://user-images.githubusercontent.com/57285121/117760406-87ce9780-b260-11eb-833e-0b01dccef510.png">   

<img width="751" alt="스크린샷 2021-05-09 오후 3 08 16" src="https://user-images.githubusercontent.com/57285121/117761015-99646f00-b261-11eb-8a0f-f92b4a2a4905.png">   

<img width="693" alt="스크린샷 2021-05-09 오후 3 08 44" src="https://user-images.githubusercontent.com/57285121/117762477-36280c00-b264-11eb-8509-0dbf188a64c1.png">   

> * mkfs.<파일시스템이름> <장치이름> :	장치에 파일시스템을 입혀줌(포맷)   
<img width="557" alt="스크린샷 2021-05-09 오후 3 09 01" src="https://user-images.githubusercontent.com/57285121/117761540-771f2100-b262-11eb-88b4-88cd16f3578e.png">   

> * mount 명령어를 통해 해당 디렉토리에 마운트 진행   

## RAID 0 구현   
<img width="726" alt="스크린샷 2021-05-11 오후 3 01 17" src="https://user-images.githubusercontent.com/57285121/117765964-c74db180-b269-11eb-89b8-2c53c2aaa3e0.png">   

<img width="681" alt="스크린샷 2021-05-11 오후 3 10 06" src="https://user-images.githubusercontent.com/57285121/117766739-ff092900-b26a-11eb-96ab-6f90add84e78.png">   

<img width="569" alt="스크린샷 2021-05-11 오후 3 11 15" src="https://user-images.githubusercontent.com/57285121/117766848-22cc6f00-b26b-11eb-8eae-792ca40097a9.png">   

<img width="723" alt="스크린샷 2021-05-11 오후 3 45 16" src="https://user-images.githubusercontent.com/57285121/117770453-e51e1500-b26f-11eb-9232-7c5c6586d010.png">   

## RAID 1 구현   
<img width="725" alt="스크린샷 2021-05-11 오후 3 31 33" src="https://user-images.githubusercontent.com/57285121/117768885-f8c87c00-b26d-11eb-8cec-d710b503a210.png">   

<img width="679" alt="스크린샷 2021-05-11 오후 3 32 09" src="https://user-images.githubusercontent.com/57285121/117768939-0ed63c80-b26e-11eb-87c0-a749904a81af.png">   

<img width="563" alt="스크린샷 2021-05-11 오후 3 33 17" src="https://user-images.githubusercontent.com/57285121/117769100-36c5a000-b26e-11eb-94d3-1c9f15ca57bd.png">   

<img width="719" alt="스크린샷 2021-05-11 오후 3 45 58" src="https://user-images.githubusercontent.com/57285121/117770529-fd8e2f80-b26f-11eb-9e15-f1ada46ec58a.png">

## RAID 5 구현   
<img width="725" alt="스크린샷 2021-05-11 오후 3 41 33" src="https://user-images.githubusercontent.com/57285121/117770001-5f01ce80-b26f-11eb-8420-6de7d383e5c3.png">   

<img width="677" alt="스크린샷 2021-05-11 오후 3 43 10" src="https://user-images.githubusercontent.com/57285121/117770176-983a3e80-b26f-11eb-8594-28257acc92e1.png">   

<img width="559" alt="스크린샷 2021-05-11 오후 3 43 59" src="https://user-images.githubusercontent.com/57285121/117770273-b4d67680-b26f-11eb-9b20-10596485131b.png">   

<img width="722" alt="스크린샷 2021-05-11 오후 3 46 50" src="https://user-images.githubusercontent.com/57285121/117770622-1bf42b00-b270-11eb-9a53-b8a48f82eb56.png">   

## RAID 6 구현   
<img width="723" alt="스크린샷 2021-05-12 오전 12 50 03" src="https://user-images.githubusercontent.com/57285121/117846000-fee54980-b2bb-11eb-9061-052892a27c20.png">   

<img width="661" alt="스크린샷 2021-05-12 오전 12 51 06" src="https://user-images.githubusercontent.com/57285121/117846165-263c1680-b2bc-11eb-8f42-fdeb7c6dcc47.png">   

<img width="562" alt="스크린샷 2021-05-12 오전 12 59 34" src="https://user-images.githubusercontent.com/57285121/117847509-5d5ef780-b2bd-11eb-916d-13a5f851ee44.png">   

<img width="720" alt="스크린샷 2021-05-12 오전 12 55 04" src="https://user-images.githubusercontent.com/57285121/117846775-b4180180-b2bc-11eb-9423-ea32f7ec0959.png">   


## RAID 0+1 구현

## RAID 1+0 구현

# RAID 구성 시 발생할 수 있는 문제들과 조치 방법 테스트
* RAID 0 2개(/dev/md0), RAID 1 2개(/dev/md1), RAID 5 3개(/dev/md5), RAID 6 4개(/dev/md6) 총 11개의 디스크가 추가되어 있는 상태
* RAID 0의 디스크 하나, RAID 1의 디스크 하나, RAID 5의 디스크 하나, RAID 6의 디스크 둘을 고장내보고 RAID Level별 특징을 확인
* RAID로 구성된 하드디스크중 하나를 제거(고장난 것과 같은 효과)
* 각 RAID Level에 임시의 testfile을 저장해 놓고 고장 시 파일들이 어떻게 되는지 확인 및 조치(결함 허용 확인)
* 테스트 전 RAID가 마운트 되어 있어야함 
* 하드디스크를 제거하고 부팅을 하게되면 응급 모드(Emergency mode)로 접속됨   
<img width="796" alt="스크린샷 2021-05-12 오후 4 11 21" src="https://user-images.githubusercontent.com/57285121/117933611-b326b480-b33c-11eb-8ab3-517c02515adf.png">   
응급 모드로 접속된 모습   

<img width="497" alt="스크린샷 2021-05-12 오후 4 13 45" src="https://user-images.githubusercontent.com/57285121/117933914-0862c600-b33d-11eb-90d2-a630ab308914.png">   
응급 모드로 접속 후 root계정으로 로그인하여 디스크의 상태를 확인. 결함 허용을 제공하지 않는 RAID 0은 사라져 있음

## RAID 0 확인   
<img width="770" alt="스크린샷 2021-05-12 오후 4 20 45" src="https://user-images.githubusercontent.com/57285121/117934815-03524680-b33e-11eb-9850-df7b9c351b31.png">   
mdadm 명령어를 통해 RAID 0이 구성되어있던 /dev/md0의 상태가 inactive로 바뀌어있고 구성 디스크가 하나밖에 없음을 확인   
   
<img width="418" alt="스크린샷 2021-05-12 오후 4 30 43" src="https://user-images.githubusercontent.com/57285121/117936097-68f30280-b33f-11eb-8c99-2d7501ee3aa6.png">   
testfile도 없어져 있음

## RAID 1 확인   
<img width="762" alt="스크린샷 2021-05-12 오후 4 23 25" src="https://user-images.githubusercontent.com/57285121/117935144-6348ed00-b33e-11eb-8864-e0baf236b11e.png">   
mdadm 명령어를 통해 RAID 1이 구성되어있던 /dev/md1의 상태가 clean, degraded(사용할 수는 있으나 이대로 사용하면 백업 기능 사용 불가)로 되어있고 디스크 하나가 제거되어 있음을 확인   

<img width="547" alt="스크린샷 2021-05-12 오후 4 32 27" src="https://user-images.githubusercontent.com/57285121/117936291-a6579000-b33f-11eb-9c3a-7b14a26e62f6.png">   
testfile이 아직 그대로 있음(결함 허용)

## RAID 5 확인   
<img width="774" alt="스크린샷 2021-05-12 오후 4 27 11" src="https://user-images.githubusercontent.com/57285121/117935661-ea966080-b33e-11eb-9913-d5997b11df1f.png">   
mdadm 명령어를 통해 RAID 5가 구성되어 있던 /dev/md5의 상태가 clean, degraded상태로 되어있고 디스크 하나가 제거되어 있음을 확인   

<img width="549" alt="스크린샷 2021-05-12 오후 4 33 48" src="https://user-images.githubusercontent.com/57285121/117936452-d56e0180-b33f-11eb-94c1-b619e6fa0409.png">   
testfile이 아직 그대로 있음(결함 허용)

## RAID 6 확인   
<img width="769" alt="스크린샷 2021-05-12 오후 4 29 03" src="https://user-images.githubusercontent.com/57285121/117935890-2b8e7500-b33f-11eb-8fa7-d8ea04f7f30c.png">   
mdadm 명령어를 통해 RAID 6이 구성되어 있던 /dev/md6의 상태가 clean, degraded상태로 되어있고 디스크 두 개가 제거되어 있음을 확인   

<img width="550" alt="스크린샷 2021-05-12 오후 4 34 45" src="https://user-images.githubusercontent.com/57285121/117936564-f6ceed80-b33f-11eb-8416-181476a2fc6a.png">   
testfile이 아직 그대로 있음(결함 허용)

# 고장난 RAID를 다시 작동 
* mdadm --run 명령어를 통해 작동   
<img width="516" alt="스크린샷 2021-05-12 오후 4 53 11" src="https://user-images.githubusercontent.com/57285121/117938980-942b2100-b342-11eb-8b72-48b0f8303806.png">   
mdadm명령어로 RAID 0, 1, 5, 6을 작동시켰으나 0은 작동이 되지 않음   

<img width="755" alt="스크린샷 2021-05-12 오후 4 54 28" src="https://user-images.githubusercontent.com/57285121/117939117-b9b82a80-b342-11eb-8793-6db1bc007e0a.png">   
상태가 active, FAILED, Not started로 나옴(사용 불가)   

<img width="756" alt="스크린샷 2021-05-12 오후 4 57 32" src="https://user-images.githubusercontent.com/57285121/117939565-26332980-b343-11eb-8dc0-1be7a8d671e5.png">   
RAID 1 (/dev/md1)은 사용 가능이긴 하나 백업 불가 상태(clean, degraded)   

<img width="773" alt="스크린샷 2021-05-12 오후 4 58 42" src="https://user-images.githubusercontent.com/57285121/117939714-4fec5080-b343-11eb-938e-d71b688d80e0.png">   
RAID 5 (/dev/md5)도 마찬가지로 clean, degraded   

<img width="753" alt="스크린샷 2021-05-12 오후 4 59 55" src="https://user-images.githubusercontent.com/57285121/117939916-7c07d180-b343-11eb-93a6-7174b1117e90.png">   
RAID 6 (/dev/md6)도 마찬가지.

* 시스템 정상 작동을 위해 응급 모드 탈출을 해야함
* RAID 0은 사용 불능 상태이므로 RAID 중지 후 영구 마운트 해제 해야함
* mdadm --stop 명령어로 RAID 중지   
<img width="403" alt="스크린샷 2021-05-12 오후 5 09 09" src="https://user-images.githubusercontent.com/57285121/117941144-c76eaf80-b344-11eb-9a38-6ef5a170e738.png">   

* /etc/fstab을 열어서 영구 마운트 해제   
<img width="489" alt="스크린샷 2021-05-12 오후 5 11 00" src="https://user-images.githubusercontent.com/57285121/117941425-07ce2d80-b345-11eb-890e-9d16d0a24129.png">   
* 재부팅 후 시스템 정상 작동   

# RAID 원상 복구 
* 고장냈던 디스크 5개를 다시 추가
* RAID 0은 추가한 디스크를 통해 재구성을 해줘야 하며 RAID 1, 5, 6은 새로운 디스크를 추가해 주기만 하면 된다.
* RAID 0 복구   
1. 새로운 디스크 추가   
2. 디스크 포맷   
3. mdadm --stop 명령어로 **기존 RAID를 중지**
4. mdadm --create 명령어로 새로 포맷한 디스크와 기존 RAID 0으로 구성되어 있던 디스크를 재구성   
<img width="851" alt="스크린샷 2021-05-14 오후 2 50 33" src="https://user-images.githubusercontent.com/57285121/118227582-bdbf8600-b4c3-11eb-8bb2-41e2632b0a26.png">   
기존 RAID를 중지해야 함(안하면 오류 뜸)

<img width="762" alt="스크린샷 2021-05-14 오후 2 51 02" src="https://user-images.githubusercontent.com/57285121/118227622-d039bf80-b4c3-11eb-8115-a11cffbf3382.png">   
기존 RAID 0 재구성 

* RAID 1, 5, 6 복구   
<img width="485" alt="스크린샷 2021-05-14 오후 2 47 42" src="https://user-images.githubusercontent.com/57285121/118227337-586b9500-b4c3-11eb-89e3-dd7c42d8677b.png">   

<img width="754" alt="스크린샷 2021-05-14 오후 2 48 39" src="https://user-images.githubusercontent.com/57285121/118227420-7b964480-b4c3-11eb-849d-01afc90a2840.png">   
RAID 1 복구

<img width="765" alt="스크린샷 2021-05-14 오후 2 54 44" src="https://user-images.githubusercontent.com/57285121/118227933-535b1580-b4c4-11eb-9d4f-d985e9a5ad3b.png">   
RAID 5 복구

<img width="763" alt="스크린샷 2021-05-14 오후 2 59 17" src="https://user-images.githubusercontent.com/57285121/118228327-f6ac2a80-b4c4-11eb-875d-11a07d731f8a.png">   
RAID 6 복구

<img width="493" alt="스크린샷 2021-05-14 오후 3 17 20" src="https://user-images.githubusercontent.com/57285121/118229752-7f2bca80-b4c7-11eb-9406-b9bda1e9392a.png">   
정상적으로 RAID 0, 1, 5, 6이 마운트 됨

<img width="563" alt="스크린샷 2021-05-14 오후 3 19 27" src="https://user-images.githubusercontent.com/57285121/118229917-c74aed00-b4c7-11eb-84ac-d0ae1bdb7032.png">   
RAID 0은 데이터가 복구되지 않았고 1, 5, 6은 정상적으로 원상 복구
