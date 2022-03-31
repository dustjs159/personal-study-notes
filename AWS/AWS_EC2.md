💻 [AWS] EC2
=============

# 💡 Amazon EC2

* AWS 클라우드 환경에서 가상의 서버를 구축하기 위한 컴퓨팅 자원을 빌려주는 **컴퓨팅 서비스**
* EC2 서비스를 통해 생성되는 가상 서버는 **인스턴스**라는 이름으로 생성 됨
* EC2 서비스의 리소스들을 조합하여 요구사항에 최적화된 인스턴스를 생성
* AWS 웹 콘솔을 통해 클릭 몇 번으로 쉽게 생성이 가능
* EC2 서비스의 리소스는 크게 세 부분으로 나눠 구성
  * Instance(Server)
  * Network & Security
  * Storage

## 📌 Instance 
* 인스턴스(Instance) : EC2 서비스로 생성되는 클라우드 환경의 **가상 서버**
  * AMI(Amazon Machine Image) 
  * 인스턴스 유형(Type)
  * 인스턴스 수명 주기
  * 인스턴스 구입 옵션
  * 태그 기능

### ✔️ AMI(Amazon Machine Image)
   
![](https://images.velog.io/images/dustjs159/post/c7223c11-14b1-4ee6-8f75-af02079aaa05/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-01-09%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2011.02.18.png)

* AMI(Amazon Machine Image) : 인스턴스를 생성하기 위해 필요한 운영체제와 그 외 필요한 소프트웨어들(웹 서버 Nginx 등)이 설치된 디스크 이미지
* AWS에서 제공하는 AMI를 커스터마이징하여 동일한 구성의 여러 인스턴스를 찍어내듯 생성 가능(필요한 소프트웨어를 인스턴스 생성할 때마다 설치하지 않아도 됨)
* EC2 생성 시 선택할 수 있는 AMI 종류 
  * Linux : Amazon Linux2, Red Hat Enterprise Linux, Ubuntu, SUSE Linux 등
  * Windows : MS Windows Server 등
* 이미 만들어져있는 AMI 외에 개인이 직접 제작하여 Marketplace에서 배포도 가능하며 이 경우에는 AMI가 안전하지 않을 수도 있기 때문에 배포자를 잘 확인하고 사용

 
### ✔️ 인스턴스 유형(Type)

<img width="301" alt="스크린샷 2021-08-16 오후 9 39 24" src="https://user-images.githubusercontent.com/57285121/129565131-d1d32318-148a-47e2-8a13-697e6fb2b35e.png">

* 생성할 인스턴스의 Type
* AWS에서는 다양한 인스턴스 Type을 제공하며 목적에 맞게 선택하여 사용
* 각 인스턴스 유형마다 그룹화(T Class, C Class, .. 등)
* 범용적 인스턴스(General) : 가장 범용적인 인스턴스 생성을 위한 인스턴스 유형. 일반적인 인스턴스를 생성하고자 할 때 선택
  * Class
    * M : Most Scenarios(General Purpose)
    * T : Turbo(Burstable)
  * T 클래스는 버스트 기능을 지원
  * 버스트 기능이란 필요한 만큼 성능을 높일 수 있는 성능 순간 확장 기능. 버스트 기능을 사용하여 기준 사용률을 초과하게 될 경우 추가 요금이 부과됨
 
* 컴퓨팅 최적화 인스턴스 : 고성능의 CPU 연산작업을 위한 인스턴스 유형
  * Class
    * C : Computing
* 메모리 최적화 인스턴스 : 메모리 상에서 큰 규모의 데이터를 처리하는 작업을 위한 인스턴스 유형
  * Class
    * R : Random-Access Memory
    * X : Extra-Large Memory
* 스토리지 최적화 인스턴스 : 로컬 스토리지의 대규모 데이터베이스에 대해 잦은 I/O가 발생하는 작업을 위한 인스턴스 유형
  * Class
    * D : Dense Storage
    * H : Hard Disk (HDD)
    * I : I/O. (NVMe, SSD)
* 가속화된 컴퓨팅 최적화 인스턴스 : GPU를 활용한 영상 처리나 그래픽 기능을 활용하기 위한 인스턴스 유형
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

### ✔️ 인스턴스 구매 옵션

* **On-Demand Instances**
  * 인스턴스를 생성하는 순간부터 초 단위로 비용을 지불하는 방식. 
  * 사용한 만큼만 비용을 지불하면 되기 때문에 종료 기간이 불확실한 경우에 사용하기 적합
* Savings Plans
  * 특정 기간(1년 or 3년)동안 사용량에 대한 비용(시간당 USD)을 고정함으로써 비용 절감 가능
* 예약 인스턴스(Reserve Instances)
  * 특정 기간동안 약정을 맺고 비용을 지불하는 일종의 정액제 요금제. 
  * 선 결제시 온디맨드 인스턴스보다 저렴하게 사용할 수 있지만 계약 기간 중 비용 환불이 되지 않기 때문에 인스턴스 사용 기간이 확실한 경우에 사용하기 적합
* 스팟 인스턴스
  * 사용중이지 않은 잉여 EC2를 사용하여 상대적으로 적은 비용으로 인스턴스 생성이 가능. AWS에서 언제든지 회수할 수 있기 때문에 그에 대한 대비책을 마련해야함.


### ✔️ 태그
   
![](https://images.velog.io/images/dustjs159/post/39de7459-917e-4163-a86b-cad4a723c460/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-01-09%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2011.24.36.png)
   
* 인스턴스를 구분하기 위한 태그
* ``Key`` 와 ``Value`` 로 구성
* 여러 인스턴스들 사이에서 특정 인스턴스만 작업을 수행하고 싶을 때 지정한 태그를 통해 해당 인스턴스만 작업 가능

### ✔️ 인스턴스의 수명 주기
   
<img width="544" alt="스크린샷 2021-08-17 오전 1 55 09" src="https://user-images.githubusercontent.com/57285121/129600700-8489a965-d112-4563-9b3b-0364ff013f0e.png">

* EC2 인스턴스는 시작 ~ 종료 사이에 다양한 상태로 전환

* 인스턴스 시작
  * 인스턴스를 시작하면 `running` 상태 이전에 먼저 `pending`상태로 전환
  * `pending` 상태에서는 비용이 청구되지 않으며 선택한 인스턴스 유형과 AMI에 따라 인스턴스 생성 준비
  * AMI의 부팅정보를 참조하여 부팅을 위한 준비를 마치면 `running` 상태로 전환되며 인스턴스 시작
  * 인스턴스가 `running` 상태가 되면서 비용이 청구

* 인스턴스 중지
  * 인스턴스가 `running` 상태일 때 중지를 하게되면 `stopping`상태를 거친 후 `stopped` 상태가 됨
  * 인스턴스에 연결되어 있던 EBS 볼륨과 볼륨 내 데이터들은 그대로 유지되며 언제든지 다시 재연결하여 사용 가능
  * 인스턴스가 `stopped` 상태일 경우에는 인스턴스 비용이 청구되지 않지만 EBS 볼륨에 대한 스토리지 비용은 청구됨. 이 때 인스턴스에 대해 변경사항(인스턴스 유형 등)을 반영 가능

* 인스턴스 종료
  * 인스턴스를 종료하면 `shutting-down` 상태를 거쳐 `terminated` 상태가 됨
  * `shutting-down`, `terminated` 두 상태 모두 비용이 청구되지 않음
  * 루트 디바이스 볼륨은 삭제되며 그 이외에 EBS 볼륨은 삭제되지 않고 유지


## 📌 Storage
   
![](https://images.velog.io/images/dustjs159/post/920c11b4-3ef5-4369-8082-54e12812dede/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-02-08%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%2012.29.30.png)

* 인스턴스의 스토리지
* 인스턴스의 루트 디바이스 볼륨과 추가할 볼륨을 지정
* 루트 디바이스에는 인스턴스 부팅을 위해 필요한 정보들이 포함
* 인스턴스의 볼륨으로 사용 가능한 스토리지 옵션
  * 인스턴스 스토어
  * **Amazon EBS(Elastic Block Store)**
* 사용 가능한 디바이스의 이름(루트 포함)은 AMI에 따라 조금씩 다름
* 가질 수 있는 루트 디바이스의 이름
  * Amazon Linux 2 : /dev/xvda
  * RHEL, Ubuntu, SUSE Linux, Windows : /dev/sda1
* 루트 디바이스 외 추가되는 스토리지의 이름은 /dev/sd[f~p]
* EC2와 함께 Amazon EFS, Amazon S3도 사용 가능

## 📌 Network & Security
   
<img width="626" alt="스크린샷 2021-08-17 오전 1 14 19" src="https://user-images.githubusercontent.com/57285121/129595422-20830f8b-e439-469a-a2a8-f1481abd67a5.png">

* 네트워크 및 보안
  * 보안 그룹
  * 키 페어
  * 탄력적 IP 주소(Elastic IP)
  * 네트워크 환경 설정(생성한 VPC와 연결)
  * 인스턴스를 배치할 **네트워크**를 설정
* 네트워크는 AWS에서 제공하는 **VPC** 서비스를 통해 설정한 범위에서 설정
* 배치할 VPC 내의 가용영역에 생성된 **서브넷**을 선택
* 서브넷을 선택하면 서브넷의 사설 IP 대역 내의 IP가 할당됨

### ✔️ 보안그룹

* 인스턴스에 대한 트래픽을 제어하는 **방화벽** 
* Inbound / Outbound 트래픽에 대해 허용할 규칙 지정
  * Inbound 규칙 : 프토토콜, 포트번호, Source IP 지정
  * Outbound 규칙 : 프로토콜, 포트번호, Destination IP 지정
  
### ✔️ 탄력적 IP

![](https://images.velog.io/images/dustjs159/post/66e28f4b-f091-432b-ad5d-76b3c045a79f/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-01-10%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%2012.52.44.png)

* **Elastic IP**
* AWS로 부터 할당받을 수 있는 **Public Static IP**
* Static IP를 탄력적으로 계정 내 다른 인스턴스에게 연결이 가능
  * 인스턴스 A에게 연결되어 있던 Static IP A를 연결 해제 후 계정 내 인스턴스 B에 연결 가능
* 할당받은 Elastic IP가 인스턴스에 되어 있지 않거나 중지된 인스턴스에 연결되어 있는 경우에는 추가 비용이 발생할 수 있음 → **한정된 Public IPv4 주소를 낭비 없이 효율적으로 사용할 수 있도록**

### ✔️ 키 페어

* SSH Key 사용
* ID, PW를 사용하여 인스턴스에 로그인 하는 방식이 아닌 AWS에서 발급받은 SSH Key를 사용하여 인스턴스에 접근
* 키 페어 분실 시 재발급

