💻 [AWS] EC2 Instance Type
=============

<img width="301" alt="스크린샷 2021-08-16 오후 9 39 24" src="https://user-images.githubusercontent.com/57285121/129565131-d1d32318-148a-47e2-8a13-697e6fb2b35e.png">

* Intance Type : 생성할 인스턴스의 유형
* AWS에서는 다양한 인스턴스 Type을 제공하며 목적에 맞게 선택하여 사용
* 각 인스턴스 유형마다 그룹화(T Class, C Class, .. 등)
* General : 가장 범용적인 인스턴스 생성을 위한 인스턴스 유형. 일반적인 인스턴스를 생성하고자 할 때 선택
  * Class
    * M : Most Scenarios(General Purpose)
    * T : Turbo(Burstable)
  * T 클래스는 버스트 기능을 지원
  * 버스트 기능이란 필요한 만큼 성능을 높일 수 있는 성능 순간 확장 기능. 버스트 기능을 사용하여 기준 사용률을 초과하게 될 경우 추가 요금이 부과됨
* 컴퓨팅 최적화 유형 : 고성능의 CPU 연산작업을 위한 인스턴스 유형
  * Class
    * C : Computing
* 메모리 최적화 유형 : 메모리 상에서 큰 규모의 데이터를 처리하는 작업을 위한 인스턴스 유형
  * Class
    * R : Random-Access Memory
    * X : Extra-Large Memory
* 스토리지 최적화 유형 : 로컬 스토리지의 대규모 데이터베이스에 대해 잦은 I/O가 발생하는 작업을 위한 인스턴스 유형
  * Class
    * D : Dense Storage
    * H : Hard Disk (HDD)
    * I : I/O. (NVMe, SSD)
* 가속화된 컴퓨팅 최적화 유형 : GPU를 활용한 영상 처리나 그래픽 기능을 활용하기 위한 인스턴스 유형
  * Class
    * G : GPU
    * P : GPU (G와 유사)
* 인스턴스 세대 표기 의미
  * a : AMD CPU
  * b : Block Storage Optimized
  * e : Extra Capacity (Storage / RAM)
  * n : Networking Optimized
  * d : Directly-Attached Instance Storage
  * g : Graviton2 Processors
  * z : High Frequency