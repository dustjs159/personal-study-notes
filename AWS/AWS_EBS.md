
💻 [AWS] EC2 - Amazon EBS
=============

# 💡 EC2 Storage - Amazon EBS

## 📌 인스턴스 스토어
* 인스턴스 스토어는 **임시적인 블록 스토리지**
* 내장 디스크
* **데이터를 영구적으로 저장하지 않음**
* 인스턴스 스토어는 인스턴스 중지 및 종료할 경우 스토리지가 증발(물론 스토리지 내 데이터들도)하기 때문에 인스턴스 유형을 변경하기 위해 인스턴스 종료 및 중지 불가 → 동적인 인스턴스 구성(기존 볼륨을 다른 인스턴스에 연결 등)이 불가능
* 과거에는 인스턴스 스토어가 EC2 인스턴스 부팅을 위한 정보들이 담겨있는 루트 디바이스였지만 Amazon EBS 출시 이후에는 루트 디바이스가 **Amazon EBS** 로 변경

## 📌 Amazon EBS
   
<img width="400" alt="스크린샷 2021-08-28 오후 11 48 50" src="https://user-images.githubusercontent.com/57285121/131221914-e6ddfae0-fe98-4279-8de6-e443e4943c51.png">

* Amazon EBS(Elastic Block Store)는 EC2 인스턴스에 연결하여 사용할 수 있는 볼륨
  * 인스턴스에 연결할 수 있는 하드디스크
* Amazon EBS는 **블록 스토리지** 형태의 스토리지 서비스
* 인스턴스에 EBS 볼륨을 연결하여 사용하기 위해서는 EBS 볼륨과 EC2 인스턴스가 같은 가용영역에 있어야 함
* Amazon EBS는 인스턴스 스토어와는 다르게 **영구적으로 데이터 보관이 가능**
* 인스턴스의 수명주기와 관계없이 지속되기 때문에 기존에 인스턴스에 연결되어 있던 EBS 볼륨을 분리하여 다른 인스턴스에 연결하여 사용이 가능하고 인스턴스 중지 및 종료할 경우에도 삭제되지 않고 필요에 따라 재사용이 가능
* **Snapshot** 기능 지원
  * Snapshot을 생성하여 볼륨 내 데이터를 백업 가능
* EC2 인스턴스 생성을 위한 AMI 선택 시 루트 디바이스 유형이 대부분 인스턴스 스토어가 아닌 Amazon EBS 로 설정되어있음 
   
<img width="556" alt="스크린샷 2021-08-28 오전 2 30 28" src="https://user-images.githubusercontent.com/57285121/131166455-d5a84aaa-74f7-4b18-a3fb-857d8a45a6ec.png">

  * 대부분의 AMI의 루트 디바이스는 EBS 볼륨을 사용
    * EBS 볼륨이 **인스턴스 중지 후 인스턴스 유형을 수정할 수 있기 때문**
    * 기존 볼륨에 대해 변동 사항이 발생하면 인스턴스 유형을 수정해야할 경우가 있는데, 이 때 EBS 볼륨은 인스턴스 중지 후 인스턴스의 유형을 변경 후에 다시 볼륨을 연결하여 사용할 수 있지만 인스턴스 스토어는 인스턴스 생성 시 최초의 인스턴스 유형을 설정하면 변경할 수 없기 때문에 대부분의 루트 디바이스가 EBS 볼륨으로 지정 
   
|특징|Amazon EBS 지원 AMI|인스턴스 스토어 지원 AMI|
|------|---|---|
|부팅 시간|빠름(1분 이하)|상대적으로 느림(5분 이하)|
|루트 디바이스 볼륨| **Amazon EBS** |인스턴스 스토어|
|데이터 지속성| **영구적**으로 보관|영구적이지 않고 임시 보관(휘발성)|
|인스턴스 유형 변경| **인스턴스 중지 후 인스턴스 유형 변경 가능** |최초 인스턴스 유형 선택 후 변경 불가|
|인스턴스 중지 및 종료|인스턴스 중지 및 종료 후 **언제든지 재시작 가능** |인스턴스 중지 및 종료 불가|
   
## 📌 Amazon EBS 볼륨 유형
   
<img width="199" alt="스크린샷 2021-08-28 오전 2 45 55" src="https://user-images.githubusercontent.com/57285121/131168209-e300880a-0fca-4397-b950-7d968c20e225.png">

* **SSD(Solid-State Drive)**
* **HDD(Hard Disk Drive)**
* 마그네틱

### ✔️ SSD(Solid-Statd Drive)

* 범용 SSD (General Purpose SSD)
  * gp3 : 볼륨당 최대 처리량(Throughtput) : 1000MiB/s
  * gp2 : 볼륨당 최대 처리량(Throughtput) : 250MiB/s
  
* IOPS 프로비저닝 SSD (Provisioned IOPS SSD)
  * io1
  * io2
   
### ✔️ HDD(Hard Disk Drive)

* 처리량 최적화 HDD (Throughtput Optimized HDD)
  * st1
* Cold HDD
  * sc1

## 📌 EBS Snapshot

* Amazon EBS는 스냅샷 기능을 제공
* 특정 시점에 대한 볼륨 스냅샷 기능을 통해 EBS 볼륨의 백업이 가능
* 생성한 EBS 볼륨의 스냅샷은 계정 간 공유 및 복제, 리전 간 복제가 가능

<img width="723" alt="스크린샷 2021-08-29 오전 12 24 05" src="https://user-images.githubusercontent.com/57285121/131222831-62538d84-8d35-4488-8ef3-d6e73829175b.png">

* EBS 볼륨의 스냅샷은 **증분식 백업**으로 저장
  * 새 스냅샷을 생성할 때는 마지막 스냅샷 이후 변경된 사항만 저장
* 증분식 백업의 과정
   
![image](https://user-images.githubusercontent.com/57285121/131222884-2f74dc20-4512-4d5c-87f5-851977f5aa82.png)
   
1. State 1에서 10 GiB의 볼륨 1 을 전체 다 스냅샷 (Snap A)생성 (첫 번째 스냅샷이라서)
2. State 2에서 볼륨 1의 데이터 10 GiB 중 4 GiB의 변동사항 발생
3. Snap B는 10 GiB중 변동사항이 발생한 4 GiB만큼만 생성하고 변동사항이 발생하지 않은 Snap A의 6 GiB를 참조하여 가져옴
4. State 3에서 2 GiB의 데이터가 추가 저장되어 총 12 GiB가 됨
5. Snap C는 추가한 2 GiB만 생성하고 나머지 6 GiB는 Snap A에서, 4 GiB는 Snap B에서 참조
6. 세 스냅샷(Snap A, B, C)을 생성하는데 필요한 총 스토리지는 16 GiB(10 + 4 + 2 GiB)

### ✔️ Amazon DLM(Data Lifecycle Manager)

* **백업의 생성, 보존, 삭제를 자동화**
* EBS Snapshot, EBS 기반 AMI에 적용하여 백업을 자동화 할 수 있음


## 📌 EBS 암호화
   
<img width="388" alt="스크린샷 2021-08-29 오전 12 54 46" src="https://user-images.githubusercontent.com/57285121/131223605-b71d2d04-c868-406c-b48b-dba39822dcd6.png">

* Amazon EBS 는 암호화 기능을 제공
* 암호화 기능을 통해 EBS 볼륨 내에 저장되어 있는 데이터를 보호할 수 있음
* 암호화된 볼륨 및 스냅샷을 생성할 때 **AWS KMS Key**를 사용
* EBS 볼륨 내 데이터, 볼륨과 인스턴스 사이의 데이터 전송 과정에서의 데이터, 볼륨으로부터 생성된 스냅샷 모두 암호화 기능이 적용
* Amazon EBS의 암호화 알고리즘은 **AES(대칭키 암호화 방식)** 