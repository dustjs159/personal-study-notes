💻 [AWS] EC2 Instance Life Cycle
================================

## 인스턴스의 생명 주기
<img width="544" alt="스크린샷 2021-08-17 오전 1 55 09" src="https://user-images.githubusercontent.com/57285121/129600700-8489a965-d112-4563-9b3b-0364ff013f0e.png">

* EC2 인스턴스는 `Launch ~ Terminate` 사이에 다양한 상태로 전환
* `Launch`
  * 인스턴스를 생성하기 위해 AMI, 인스턴스 유형, 네트워크 설정 등을 거쳐서 Launch 하게 되면 즉각적으로 가동되는 것이 아닌 `Pending` 상태를 거쳐 가동됨
  * `Pending` 상태에서는 비용이 청구되지 않음
* `Running` : 인스턴스가 정상적으로 가동중인 상태
  * 비용이 청구됨
* `Rebooting` : 인스턴스 재부팅 중...
* `Stopped` : 인스턴스 중지
  * EBS 볼륨 기반의(root 볼륨이 EBS 볼륨인) 인스턴스만 가능
    * 인스턴스 스토어 기반의 인스턴스는 볼륨의 데이터가 휘발성이기 때문에 `Stop` 해도 볼륨 재사용 불가 및 데이터 증발
  * 비용이 청구되지 않음(단, 인스턴스에 Attach된 EBS 볼륨의 비용은 청구됨)
* `Terminated` : 인스턴스 종료

## Reboot vs Stop/Start
* `Reboot` 은 호스트(Physical)가 변경 되지 않음(단순 재시작)
  * 인스턴스의 기존 정보(Private IP 등) 모두 유지(인스턴스 스토어 볼륨 마저도)
* `Stop/Start` 는 호스트가 변경될 수도 있고, 변경되지 않을 수도 있음
  * Private IP는 유지되며 Public IP는 변경될 수 있음

## Stop / Termination Protection
* 실수로 인스턴스를 중지하거나 삭제되는 것을 방지하기 위한 옵션
* `Stop` / `Termination Protection` 옵션이 활성화된 인스턴스는 중지 및 삭제 불가능
* 옵션이 활성화된 인스턴스를 중지 및 삭제하기 위해서는 옵션을 비활성화해야 함.

## Hibernate
* 최대 절전 모드
* 인스턴스 `Stop` 시 OS가 인스턴스의 RAM에 있는 데이터들을 루트 디바이스로 옮겨서 저장하고 `Stopped` 상태가 됨
* 인스턴스 `Start` 시 OS가 부팅 과정에서 루트 디바이스에 있던 RAM 데이터들을 읽고 시작
* 인스턴스 중지시 최대 절전 모드를 실행하기 위해서는 루트 EBS 볼륨이 메모리의 데이터를 저장할 여유 공간이 있어야하고 암호화 설정이 되어있어야 함