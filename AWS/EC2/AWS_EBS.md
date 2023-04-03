
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
  * 인스턴스에 연결할 수 있는 디스크
* Amazon EBS는 **블록 스토리지** 형태의 스토리지 서비스
* 인스턴스에 EBS 볼륨을 연결하여 사용하기 위해서는 EBS 볼륨과 EC2 인스턴스가 같은 가용영역에 있어야 함
* Amazon EBS는 인스턴스 스토어와는 다르게 **영구적으로 데이터 보관이 가능**
* 인스턴스의 수명주기와 관계없이 지속되기 때문에 기존에 인스턴스에 연결되어 있던 EBS 볼륨을 분리하여 다른 인스턴스에 연결하여 사용이 가능하고 인스턴스 중지 및 종료할 경우에도 삭제되지 않고 필요에 따라 재사용이 가능
* **Snapshot** 기능 지원
  * Snapshot을 생성하여 볼륨 내 데이터를 백업 가능
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

* **SSD(Solid-State Drive)**
  * General-Purpose SSD(gp2 / gp3)
      * gp3는 IOPS / Throughput 최소/최대 값이 있음
      * 최소 3000 IOPS, 125MiB/s (보다 크면 비용 청구)
  * Provisioned IOPS (io1 / io2)
      * 작은 크기의 데이터를 빠르게 처리하고자 할 때 사용
* **HDD(Hard Disk Drive)**
  * Throughput-Optimized HDD (st1)
      * 큰 크기의 데이터를 처리하고자 할 때 사용
  * Cold HDD (sc1)
      * 자주 액세스 하지 않는 데이터를 보관할 때 사용

## 📌 EBS Snapshot

* Amazon EBS는 스냅샷 기능을 제공
* 특정 시점에 대한 볼륨 스냅샷 기능을 통해 EBS 볼륨의 백업이 가능
* 생성한 EBS 볼륨의 스냅샷은 계정 간 공유 및 복제, 리전 간 복제가 가능

<img width="723" alt="스크린샷 2021-08-29 오전 12 24 05" src="https://user-images.githubusercontent.com/57285121/131222831-62538d84-8d35-4488-8ef3-d6e73829175b.png">

* EBS 볼륨의 스냅샷은 **증분식 백업**으로 저장
  * 새 스냅샷을 생성할 때는 마지막 스냅샷 이후 변경된 사항만 저장

## 📌 EBS 볼륨의 성능 평가 기준
* IOPS(Input/Output operations Per Second)
* Throughput (처리량)
* **IOPS와 Throughput의 차이점**

<img width="997" alt="스크린샷 2022-11-13 오후 5 23 11" src="https://user-images.githubusercontent.com/57285121/201512690-08540cba-93c9-4e1c-9c48-a918501ac912.png">

<img width="1005" alt="스크린샷 2022-11-13 오후 5 24 21" src="https://user-images.githubusercontent.com/57285121/201512723-2c1d9ee8-4c21-471c-9bcb-89b553431d16.png">

<img width="1001" alt="스크린샷 2022-11-13 오후 5 25 10" src="https://user-images.githubusercontent.com/57285121/201512746-6819b5d3-b63f-40d4-beed-a870da1b439b.png">

```vim
즉, 작은 크기의 데이터를 빠른 속도로 처리하기 위해서는 IOPS가 높아야 하고 처리해야 할 데이터의 크기가 큰 경우에는 Throughput이 높아야 함. 
```

### ✔️ EBS 볼륨 증설 작업
* 웹 콘솔에서 디스크의 크기를 늘려도 직접 EC2에 접속하여 크기를 확인해보면 크기가 늘어나지 않은 것을 확인할 수 있음
    * `df -Th` 커맨드로 확인해봐도 그대로
    * `lsblk`  커맨드로 확인하면 디스크 용량이 늘어나 있는 것을 확인할 수 있다 
* 이것은 디스크의 크기는 늘어나긴 했으나, 파티션과 파일시스템의 크기가 늘어나지 않아서 그런 것
* 직접 인스턴스에서 파티션과 파일시스템의 크기를 늘려줘야 함

```
# root 계정에서 실행

# 파티션 증설
growpart {partition name}

# 파일시스템 확장
resize2fs {partition name} # ext4
xfs_growfs {partition name} # xfs
```
* 주의 사항
    * 볼륨을 생성하고 파티션을 생성할 때 파티션 유형이 MBR일 경우 파티션 크기가 2TB 초과하면 더 이상 늘어나지 않음 → GPT 파티션 유형으로 변경 후 증설 가능
    * 디스크를 GPT 유형으로 만드는 방법
```bash
gdisk {device name}
```

### ✔️ EBS 볼륨을 LVM을 사용하여 묶기
* LVM : Logical Volume Manager
* 논리적인 볼륨을 만들어, 디바이스들을 하나로 묶고 크기를 나눠서 사용
* LVM으로 볼륨을 묶어서 사용했을 때 장점
    * 용량 조절이 쉬움
    * 디스크 성능이 향상됨
```
1. 물리 볼륨(PV) 생성
2. 볼륨 그룹(VG) 생성, VG에 PV 추가
3. LVM에 LV, Mount Point 생성
4. 파일 시스템 생성, 마운트
5. LV 크기 조정
```
* 참조
  * https://aws.amazon.com/ko/premiumsupport/knowledge-center/create-lv-on-ebs-partition/

### ✔️ EBS 볼륨 비용 절감 방안
* 일단 안쓰는거 먼저 삭제하는게 가장 먼저 해야할 방법(당연히)
* 그다음에는 gp2 → gp3 이전
    * gp3가 GB당 비용이 더 저렴
    * 추가로 gp3는 기본적으로 3000 IOPS를 제공하는데 반해 gp2는 GB당 3 IOPS가 제공이 됨
    * 즉, gp2의 용량이 1TB이 되는 순간부터 gp3와 만나게 되는데 1TB 미만의 디스크는 gp3를 쓰는 것이 비용이 더 저렴할 뿐더러 성능도 더 좋다.
    * 디스크의 용량이 1TB를 넘어가는 순간부터는 gp3의 비용 이점이 조금씩 줄어들 수도 있다. (그래도 더 싸다)
* 참조
    * https://silashansen.medium.com/looking-into-the-new-ebs-gp3-volumes-8eaaa8aff33e 
    * https://www.whatap.io/ko/blog/83/
* AWS CLI로 사용해보자
```bash
aws ec2 modify-volume --volume-type gp3 --volume-id vol-******
```
