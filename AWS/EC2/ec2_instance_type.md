💻 [AWS] EC2 Instance Type
==========================

# 인스턴스 유형의 종류
<img width="301" alt="스크린샷 2021-08-16 오후 9 39 24" src="https://user-images.githubusercontent.com/57285121/129565131-d1d32318-148a-47e2-8a13-697e6fb2b35e.png">

* Intance Type : 생성할 인스턴스의 유형
* AWS에서는 다양한 인스턴스 Type을 제공하며 목적에 맞게 선택하여 사용
* 각 인스턴스 유형마다 그룹화(T Class, C Class, .. 등)
* General : 가장 범용적인 인스턴스 생성을 위한 인스턴스 유형. 일반적인 인스턴스를 생성하고자 할 때 선택
  * M : Most Scenarios(General Purpose)
  * T : Turbo(Burstable)
    * T 클래스는 버스트 기능을 지원
    * 버스트 기능이란 필요한 만큼 성능을 높일 수 있는 성능 순간 확장 기능. 버스트 기능을 사용하여 기준 사용률을 초과하게 될 경우 추가 요금이 부과됨
* 컴퓨팅 최적화 유형 : 고성능의 CPU 연산작업을 위한 인스턴스 유형
  * C : Computing
* 메모리 최적화 유형 : 메모리 상에서 큰 규모의 데이터를 처리하는 작업을 위한 인스턴스 유형
  * R : Random-Access Memory
  * X : Extra-Large Memory
* 스토리지 최적화 유형 : 로컬 스토리지의 대규모 데이터베이스에 대해 잦은 I/O가 발생하는 작업을 위한 인스턴스 유형
  * D : Dense Storage
  * H : Hard Disk (HDD)
  * I : I/O. (NVMe, SSD)
* 가속화된 컴퓨팅 최적화 유형 : GPU를 활용한 영상 처리나 그래픽 기능을 활용하기 위한 인스턴스 유형
  * G : GPU
  * P : GPU (G와 유사)

# 인스턴스 유형의 표기 의미
* a : AMD CPU
* b : Block Storage Optimized
  * EBS 볼륨 최적화.
* e : Extra Capacity (Storage / RAM)
* n : Networking Optimized
* d : Directly-Attached Instance Storage
* g : Graviton2 Processors
* z : High Frequency

# T Class의 Burst 기능과 Credit에 대하여
인스턴스의 CPU 사용률이 아래와 같다고 가정해보자.

<img width="676" alt="스크린샷 2023-05-31 오전 12 38 12" src="https://github.com/dustjs159/Study/assets/57285121/c14a11b2-740d-481b-acfc-c6af5ae9c71a">

불규칙적으로 CPU가 튀는 경우가 발생할 때 인스턴스를 증설하기에는 비용 혹은 가용성에 이슈가 발생할 수도 있다. 이러한 경우를 대비하여 T 클래스의 인스턴스 유형은 버스트 모드를 지원한다.





