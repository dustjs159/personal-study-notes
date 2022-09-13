
💻 [AWS] AWS VPC
=================
# 💡 AWS VPC 

* AWS VPC(Virtual Private Cloud) : AWS의 **가상의 사설 네트워킹** 서비스
* 논리적으로 독립되어 있는 사설 네트워크 망을 구성할 수 있고 구성한 망에 AWS의 서비스(e.g. EC2 인스턴스)를 배치할 수 있음
* 기존 데이터 센터의 망 구성과 유사
  * 온프레미스 환경에서 서버 랙(Rack)이라고 보면 된다.

# 💡 VPC 주요 개념

* VPC 서비스를 사용하여 네트워크를 구성할 때 알아야 할 주요 개념들 
  * VPC
    * ENI(Elastic Network Interface)
  * Subnet
  * Routing Table
  * Internet Gateway
  * NAT Gateway
  * Security Group(SG) & Network Access Control List(ACL)
  * DHCP(Dynamic Host Configuration Protocol)
  * Elastic IP
  * VPC Endpoint(Private Link)
  * VPC Peering
  * Transit Gateway

# 💡 VPC 기본 수칙

* VPC 리소스에 대해 알기 전 기본적인 수칙.
* 이 4가지를 기억하고 VPC 서비스를 스터디하면 조금 더 와닿지 않을까 싶다.
```
 1. VPC 위에 서비스를 올리기 위해서는 반드시 ENI가 필요하다.
 2. ENI는 반드시 보안 그룹(SG)을 수반한다.
 3. ENI를 생성하기 위해서는 서브넷이 존재해야 한다.
 4. 서브넷이 존재하기 위해서는 VPC가 존재해야 한다.
 5. VPC내의 서브넷들은 최초 생성 시에 Routing Table과 Network ACL이 자동으로 붙는다. (다른 것으로 교체 가능하다)
```

## 📌 VPC(Virtual Private Cloud)

* AWS에서 제공하는 네트워킹 서비스
* Region Level
  * 하나의 리전에 여러 VPC가 포함되며 여러 리전에 중복 포함될 수 없음!
* **CIDR(Classless Inter-Domain Routing)** 표기법을 사용하여 IPv4 주소를 표기
  * CIDR 표기법 : 네트워크 영역 + 호스트 영역으로 구성되어 있는 IP 주소에서 네트워크 영역을 숫자로 표기하는 방법(e.g. IPv4 Address가 `10.0.3.0/16`일 때 `10.0` 까지가 네트워크 영역, 그 뒤 `3.0`이 호스트 영역)
* VPC에서 사용 가능한 Private IP 대역 : RFC 1918에 명시되어 있는 Private IP Range
  * `10.0.0.0/16 ~ /28`
  * `172.16.0.0/16 ~ /28`
  * `192.168.0.0/16 ~ /28`

### ✔️ ENI (Elastic Network Interface)

* 네트워크 인터페이스
  * 가상의 NIC라고 보면 된다.
* 인스턴스를 생성할 때 선택한 VPC CIDR Block 내에서 IP를 할당 받는 대상
* 이게 없으면 IP를 할당 받지 못하니 당연히 네트워크 통신이 되지 않음!
* 인스턴스에 Attach 및 Detach 가능
* 하나의 인스턴스에 여러 ENI를 Attach할 수 있지만 하나의 ENI를 여러 인스턴스에 Attach할 수 없음
  * 1:N 관계
* **보안 그룹(SG)이 Attach 되는 지점**

### ✔️ 기본 VPC 삭제

* AWS 계정을 생성하고 VPC 서비스를 확인해보면 별도의 VPC를 생성하지 않았음에도 해당 리전에  IPv4 CIDR가 `172.31.0.0/16` 인 VPC가 있음

![](https://images.velog.io/images/dustjs159/post/f0332ff4-3d16-44d1-88f3-9b2eddf1400d/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-03-07%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2010.54.40.png)

* 이것이 ``default VPC`` 인데, 네트워크 뿐 만 아니라 인프라를 구축할 때 이 VPC를 지워주도록 한다. 
* 첫 번째 이유로는 리전 당 생성할 수 있는 VPC의 수는 5개(default 값이며 조정이 가능하긴 함)로 제한. 그런데 이 ``default VPC`` 가 존재한다면 생성할 수 있는 VPC의 수 가 하나 줄어듦. 여러 대역의 네트워크 환경을 구성해야할 때 방해가 될 수도 있기에, 지워주도록 한다.
* 두 번째 이유로는 EC2 인스턴스 등 여러 AWS 서비스들을 사용하고자 할 때, VPC가 ``default VPC`` 로 설정되어 있는 경우가 있는데, 자칫 엉뚱한 대역에 서비스를 배치하게 될 수도 있으므로 지워준다.

![](https://images.velog.io/images/dustjs159/post/94f8ccff-1825-45af-a7c1-f2b375fe7425/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-03-07%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2011.12.06.png)

(EC2 인스턴스를 생성하려고 하는데 VPC가 ``default VPC``로 설정되어 있는 경우)

## 📌 Subnet

![Untitled 4](https://user-images.githubusercontent.com/57285121/161435205-00c5717f-600b-455b-a8a6-99cbf968910a.png)

* Subnet : VPC를 작은 단위로 분할한 IP 주소 범위
* Availability Zone(AZ) Level
* 서브넷은 가용 영역당 하나씩 생성
  * 고가용성을 위해 서브넷을 여러 가용영역에 생성하는 것이 best practice
* 서브넷을 목적에 따라 크게 세 가지의 서브넷으로 분류 가능
  * Public 서브넷 : 인터넷 외부에서 접속 가능
    * Default Gateway : IGW
  * Private 서브넷 : 인터넷 외부에서 접속은 불가능하나 내부에서 인터넷과 통신 가능
    * Default Gateway : NAT GW
  * Local 서브넷 : 인터넷 외부에서 접근 불가능 + 내부에서도 인터넷과 통신 불가능
    * Default Gateway : Local
 

### ✔️ **Public Subnet** & **Private Subnet**

![Untitled 6](https://user-images.githubusercontent.com/57285121/161435271-e878a321-1521-4f32-ad7a-d172b5ee4288.png)

* 외부 인터넷과의 연결 여부에 따라 Public / Private 서브넷을 구분
* Public 서브넷 내 리소스들은 외부 인터넷과 연결
* Private 서브넷 내 리소스들은 외부 인터넷과 차단


## 📌 Routing Table

![Untitled 8](https://user-images.githubusercontent.com/57285121/161435365-00fddcf9-7983-4266-98cc-716eb1dfde69.png)

* 서브넷 내에서의 라우팅(Routing) 규칙
* 서브넷마다 각각 다른 Routing Table을 정의하고 Table의 내용에 따라 해당 서브넷이 Public or Private이 되는지 결정하게 됨
* Table의 내용에는 다음 홉(Hop)으로 갈 수 있는 목적지들의 리스트가 담겨있음
* VPC를 생성하게 되면 자동으로 메인 라우팅 테이블이 생성되는데 서브넷에 별도의 라우팅 테이블을 연결하지 않았다면, 메인 라우팅 테이블의 적용을 받음

## 📌 Internet Gateway

![Untitled 9](https://user-images.githubusercontent.com/57285121/161435551-ebaf37a6-ee4b-42b8-9146-fec5b1ddc2fa.png)

* 외부 인터넷과 통신하기 위한 Gateway
  * 외부로 나가거나 외부에서 들어오는 게이트웨이 역할

## 📌 NAT Gateway

![Untitled 10](https://user-images.githubusercontent.com/57285121/161435576-e01ed955-515b-43e7-a9d6-3e156ced5a6d.png)

* NAT 기능을 수행하는 Gateway 
  * Private 서브넷에서 인터넷과 통신이 가능

## 📌 Security Group & Network Access Control List(ACL)

<img width="595" alt="스크린샷 2021-08-23 오전 2 38 00" src="https://user-images.githubusercontent.com/57285121/130364617-cb599b6c-df73-424c-84ee-ea367c28a24d.png">
   
* 보안 그룹(Security Group)과 네트워크 ACL(Access Control List)은 VPC 내 서브넷과 인스턴스에 대한 인바운드/아웃바운드 트래픽의 허용 및 거부 규칙을 제어하는 가상의 **방화벽**역할
* 보안 그룹은 인스턴스 단위로 설정, ACL은 서브넷 단위로 설정.
* 보안 그룹은 White List
  * 기본적으로 List에 등록되어 있지 않는 트래픽에 대해서는 `Deny`
  * List에 등록되어 있는 트래픽은 `Allow`
  * `Stateful`
  * 인스턴스 당 보안그룹 quota : 5
* ACL은 Black List
  * List에 등록되어 있지 않는 트래픽에 대해서는 `Allow`
  * List에 등록되어 있는 트래픽들은 `Deny`
  * `Stateless`

* 인바운드/아웃바운드 규칙은 적용할 **프로토콜**과 **포트번호**단위로 접근 규칙을 설정합니다. 포트번호는 **Well-Known Port**를 사용합니다.
   

### ✔️ Stateful / Stateless
* Stateful : 요청 정보를 저장하여 **인바운드 규칙에 따라 허용된 트래픽은 별도의 아웃바운드 규칙 없이도 인바운드 트래픽의 요청에 응답** 
  * e.g. 인바운드 규칙에 http 80번 포트가 허용되어 있으면 아웃바운드 규칙 설정 없이도 요청에 응답할 수 있습니다.   
* Stateless : 요청 정보를 따로 저장하지 않기 때문에 응답하는 트래픽의 상태과 상관없이 인바운드/아웃바운드 규칙을 따르며 허용되는 인바운드 트래픽에 대한 응답은 **인바운드 규칙에 상관없이 아웃바운드 규칙을 따름**   
  * e.g. 인바운드 규칙에 http 80번 포트가 허용되어 있더라도 아웃바운드 규칙에 http 80번 포트가 허용되어 있지 않으면 요청에 응답할 수 없음


## 📌 Elastic IP

* 탄력적 IP

## 📌 VPC Endpoint

* Private Link

# 💡 VPC 네트워킹 기본 수칙

1. VPC가 가장 먼저 생성되어야 하고 그 다음에 서브넷이 생성되어야 함

2. 서브넷이 생성되어야만 인스턴스에 Attach할 ENI를 생성할 수 있음

3. ENI는 반드시 보안 그룹(SG)을 가지고 있어야 함(즉 ENI = SG 붙는 지점)

4. VPC 내에 생성된 서브넷들은 최소 1개 이상의 네트워크 ACL, Routing Table이 자동으로 연결됨( 변경 가능)