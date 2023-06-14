💻 [AWS] EBS Volume
===================

(인스턴스 스토어에 대한 설명은 제외하겠습니다.)

<img width="400" alt="스크린샷 2021-08-28 오후 11 48 50" src="https://user-images.githubusercontent.com/57285121/131221914-e6ddfae0-fe98-4279-8de6-e443e4943c51.png">

* Amazon EBS(Elastic Block Store) Volume : 인스턴스에 연결하여 사용할 수 있는 **블록 스토리지**
  * Amazon EBS는 인스턴스 스토어와는 다르게 **영구적으로 데이터 보관이 가능**
    * 인스턴스의 수명주기와 관계없이 지속되기 때문에 기존에 인스턴스에 연결되어 있던 EBS 볼륨을 분리하여 다른 인스턴스에 연결하여 사용이 가능하고 인스턴스 중지 및 종료할 경우에도 삭제되지 않고 필요에 따라 재사용이 가능
  * **Snapshot** 기능 지원
  * 대부분의 AMI의 루트 디바이스는 EBS 볼륨을 사용
  * EBS 볼륨이 **인스턴스 중지 후 인스턴스 유형을 수정할 수 있기 때문**
  * 기존 볼륨에 대해 변동 사항이 발생하면 인스턴스 유형을 수정해야할 경우가 있는데, 이 때 EBS 볼륨은 인스턴스 중지 후 인스턴스의 유형을 변경 후에 다시 볼륨을 연결하여 사용할 수 있지만 인스턴스 스토어는 인스턴스 생성 시 최초의 인스턴스 유형을 설정하면 변경할 수 없기 때문에 대부분의 루트 디바이스가 EBS 볼륨으로 지정
  * AZ Level
* EBS 볼륨의 디바이스 이름은 OS마다 조금씩 차이가 있음
  * Amazon Linux 2 : `/dev/xvda`
  * RHEL, Ubuntu, SUSE Linux, Windows : `/dev/sda1`
   
## EBS Volume Type
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

## EBS Volume Snapshot
* EBS Snapshot : 특정 시점에 대한 백업본
* EBS 볼륨 백업 목적으로 스냅샷을 생성하여 복원 가능
  * 생성한 EBS 볼륨의 스냅샷은 계정 간 공유 및 복제, 리전 간 복제가 가능
* EBS 볼륨의 스냅샷은 **증분식 백업**으로 저장
  * 새 스냅샷을 생성할 때는 마지막 스냅샷 이후 변경된 사항만 저장
* 복원할 일이 많이 없는 스냅샷은 Archive화 하여 비용 절감 가능
* 스냅샷 Recycle bin : 스냅샷 휴지통. 실수로 스냅샷을 삭제하는 경우를 대비하여 복구 가능한 휴지통에 저장하고 보관기간 이후에는 휴지통에서 삭제됨

## EBS Volume 성능 지표
* IOPS(Input/Output operations Per Second)
* Throughput (처리량)

### IOPS vs Throughput
* EBS 볼륨의 성능 지표인 IOPS와 Throughput의 차이점
<img width="997" alt="스크린샷 2022-11-13 오후 5 23 11" src="https://user-images.githubusercontent.com/57285121/201512690-08540cba-93c9-4e1c-9c48-a918501ac912.png">

<img width="1005" alt="스크린샷 2022-11-13 오후 5 24 21" src="https://user-images.githubusercontent.com/57285121/201512723-2c1d9ee8-4c21-471c-9bcb-89b553431d16.png">

<img width="1001" alt="스크린샷 2022-11-13 오후 5 25 10" src="https://user-images.githubusercontent.com/57285121/201512746-6819b5d3-b63f-40d4-beed-a870da1b439b.png">

```vim
즉, 작은 크기의 데이터를 빠른 속도로 처리하기 위해서는 IOPS가 높아야 하고 처리해야 할 데이터의 크기가 큰 경우에는 Throughput이 높아야 함. 
```

## EBS Volume Modify
* 콘솔에서 인스턴스에 Attach된 디스크의 크기를 늘려도 직접 인스턴스에 접속하여 크기를 확인해보면 크기가 늘어나지 않은 것을 확인할 수 있음
    * `df -Th` 커맨드로 확인해봐도 그대로
    * `lsblk`  커맨드로 확인하면 디스크 용량이 늘어나 있는 것을 확인할 수 있다 
* 이것은 디스크의 크기는 늘어나긴 했으나, 파일시스템의 크기가 늘어나지 않아서 그런 것
* 직접 인스턴스에서 파일시스템의 크기를 늘려줘야 함

```
# root 계정에서 실행

# 파티션 증설 (파티션을 나누지 않고 볼륨 전체를 마운트하여 사용중인 경우 Skip)
growpart {device name} {n} # n : n번째 파티션.

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
* 하지만 IOPS, Throughput 조정은 일정 시간이 필요하지만 무중단으로 가능하다. 


## LVM으로 EBS Volume 묶어 사용하기
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

## EBS Volume 비용 절감 방안
* 일단 안쓰는거 먼저 삭제하는게 가장 먼저 해야할 방법(당연히)
* 그다음에는 gp2 → gp3 이전
    * gp3가 GB당 비용이 더 저렴
    * 추가로 gp3는 기본적으로 3000 IOPS를 제공하는데 반해 gp2는 GB당 3 IOPS가 제공이 됨
    * 즉, gp2의 용량이 1TB이 되는 순간부터 gp3와 만나게 되는데 1TB 미만의 디스크는 gp3를 쓰는 것이 비용이 더 저렴할 뿐더러 성능도 더 좋다.
    * 디스크의 용량이 1TB를 넘어가는 순간부터는 gp3의 비용 이점이 조금씩 줄어들 수도 있다. (그래도 더 싸다)
* 참조
    * https://silashansen.medium.com/looking-into-the-new-ebs-gp3-volumes-8eaaa8aff33e 
    * https://www.whatap.io/ko/blog/83/

## DLM - EBS Volume Backup
* 백업 정책을 생성하고 정책에 해당하는 인스턴스 대상의 EBS 볼륨을 정책에 따라 백업
  * 태그 등등...
