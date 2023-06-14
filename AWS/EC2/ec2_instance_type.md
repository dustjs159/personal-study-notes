💻 [AWS] EC2 Instance Type
==========================

* 인스턴스 유형 : 물리적인 장비로부터 VM을 생성할 때 VM에 할당할 리소스(vCPU, Memory 등)의 양
  * AWS에서는 다양한 인스턴스 유형을 제공하며 목적에 맞게 선택하여 사용

## 인스턴스 유형 naming convention
<img width="379" alt="스크린샷 2023-06-03 오후 1 18 38" src="https://github.com/dustjs159/Study/assets/57285121/37770e2f-0946-4cad-afc0-eeb843e4dc56">

* Instance Family : 인스턴스에서 실행할 app의 특성에 따라 5개의 유형으로 구분
  * 범용 인스턴스 유형 : 가장 범용적으로 사용할 수 있는 인스턴스 유형
    * m : Most Scenarios
    * t : Turbo. **버스트 모드 지원 가능**
  * 컴퓨팅 최적화 유형 : 범용 인스턴스 유형보다 메모리가 더 적지만 가격이 저렴. 그렇기에 메모리보다 cpu가 더 많이 필요한 경우에 고려해볼 수 있음.
    * c : Computing
  * 메모리 최적화 유형 : 범용 인스턴스 유형보다 cpu 수가 더 적지만 가격이 저렴. 그렇기에 cpu보다 메모리가 더 많이 필요한 경우에 고려해볼 수 있음.
    * r : RAM
    * x : Extra-Large Memory
  * 스토리지 최적화 유형 : 디스크 I/O가 자주 발생하는 app에 적합. (많이 안써봄)
    * d : Dense Storage
    * h : hdd
    * i : I/O. (NVMe, SSD)
  * 컴퓨팅 가속화 유형 : 그래픽 처리 등 GPU 사용해야할 때 사용. (많이 안써봄)
    * g : GPU
* Instance Generation
* Attribute
  * a : AMD CPU
  * b : EBS 볼륨 최적화
  * e : Extra Capacity (Storage or Memory)
  * n : Networking Optimized
  * d : 인스턴스 스토어 (내장 디스크)
  * g : Graviton2 Processors (ARM Architecture)
  * z : High Frequency
* Instance Size


## T Family의 Burst 기능과 Credit에 대하여
인스턴스의 CPU 사용률이 아래와 같다고 가정해보자.

<img width="676" alt="스크린샷 2023-05-31 오전 12 38 12" src="https://github.com/dustjs159/Study/assets/57285121/c14a11b2-740d-481b-acfc-c6af5ae9c71a">

불규칙적으로 CPU가 튀는 경우가 발생할 때 인스턴스를 증설하기에는 비용 혹은 가용성에 이슈가 발생할 수도 있다. 이러한 경우를 대비하여 T 패밀리의 인스턴스 유형은 버스트 모드를 지원한다.


유용한 사이트 발견
* 인스턴스 유형 정보 파악 사이트 : https://instances.vantage.sh/?region=ap-northeast-2