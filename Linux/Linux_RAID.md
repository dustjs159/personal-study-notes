RAID
====================================
RAID(Redundnat Array of Independent Disk)
------------------------------------

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
> * --raid-devices=n <장치이름1, 2 ... n> 	: RAID로 사용할 장치 개수와 이름   


### Linear RAID 구현   
<img width="878" alt="스크린샷 2021-05-09 오후 3 07 28" src="https://user-images.githubusercontent.com/57285121/117760406-87ce9780-b260-11eb-833e-0b01dccef510.png">   

<img width="751" alt="스크린샷 2021-05-09 오후 3 08 16" src="https://user-images.githubusercontent.com/57285121/117761015-99646f00-b261-11eb-8a0f-f92b4a2a4905.png">   

<img width="693" alt="스크린샷 2021-05-09 오후 3 08 44" src="https://user-images.githubusercontent.com/57285121/117762477-36280c00-b264-11eb-8509-0dbf188a64c1.png">   

> * mkfs.<파일시스템이름> <장치이름> :	장치에 파일시스템을 입혀줌(포맷)   
<img width="557" alt="스크린샷 2021-05-09 오후 3 09 01" src="https://user-images.githubusercontent.com/57285121/117761540-771f2100-b262-11eb-88b4-88cd16f3578e.png">   

> * mount 명령어를 통해 해당 디렉토리에 마운트 진행   

### RAID 0 구현   
<img width="719" alt="스크린샷 2021-05-09 오후 3 25 24" src="https://user-images.githubusercontent.com/57285121/117761264-07109b00-b262-11eb-9392-6582f46c8948.png">   

### RAID 1 구현   
<img width="721" alt="스크린샷 2021-05-09 오후 3 51 59" src="https://user-images.githubusercontent.com/57285121/117761338-23acd300-b262-11eb-9005-942fbc70a621.png">   

### RAID 5 구현

### RAID 6 구현

### RAID 0+1 구현

### RAID 1+0 구현




