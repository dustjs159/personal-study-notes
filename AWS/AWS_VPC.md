
💻 AWS VPC
===============
# 💡 AWS VPC 

* AWS VPC(Virtual Private Cloud) : AWS의 **가상의 사설 네트워킹** 서비스
* 논리적으로 독립되어 있는 사설 네트워크 망을 구성할 수 있고 구성한 망에 AWS의 서비스(e.g. EC2 인스턴스)를 배치할 수 있음
* 기존 데이터 센터의 망 구성과 유사

# 💡 VPC Resource

* VPC 서비스를 사용하여 네트워크 망을 구성할 때 사용하는 VPC 리소스 및 개념
  * VPC
  * Subnet
  * Route Table
  * Internet Gateway
  * NAT Gateway
  * Security Group(SG) & Network Access Control List(ACL)
  * Elastic IP
  * VPC Endpoint
  * DHCP(Dynamic Host Configuration Protocol)
 

## 📌 VPC(Virtual Private Cloud)

* AWS에서 제공하는 네트워크 서비스
  * VPC의 리소스를 사용하여 퍼블릭 클라우드 환경에서 망 구축 가능
* **CIDR(Classless Inter-Domain Routing)** 표기법을 사용하여 IPv4 주소를 표기
  * CIDR 표기법 : 네트워크 영역 + 호스트 영역으로 구성되어 있는 IP 주소에서 네트워크 영역을 숫자로 표기하는 방법(e.g. IPv4 Address가 `10.0.3.0/16`일 때 `10.0` 까지가 네트워크 영역, 그 뒤 `3.0`이 호스트 영역)
* VPC에서 사용 가능한 Private IP 대역 : RFC 1918에 명시되어 있는 Private IP Range
  * `10.0.0.0/16 ~ /28`
  * `172.16.0.0/16 ~ /28`
  * `192.168.0.0/16 ~ /28`

### ✔️ 기본 VPC 삭제

* AWS 계정을 생성하고 VPC 서비스를 확인해보면 별도의 VPC를 생성하지 않았음에도 해당 리전에  IPv4 CIDR가 `172.31.0.0/16` 인 VPC가 있음

![](https://images.velog.io/images/dustjs159/post/f0332ff4-3d16-44d1-88f3-9b2eddf1400d/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-03-07%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2010.54.40.png)

* 이것이 ``default VPC`` 인데, 네트워크 뿐 만 아니라 인프라를 구축할 때 이 VPC를 지워주도록 합니다. 
* 첫 번째 이유로는 리전 당 생성할 수 있는 VPC의 수는 5개(default 값이며 조정이 가능하긴 함)로 제한됩니다. 그런데 이 ``default VPC`` 가 존재한다면 생성할 수 있는 VPC의 수 가 하나 줄어듭니다. 여러 대역의 네트워크 환경을 구성해야할 때 방해가 될 수도 있기에, 지워주도록 합니다.
* 두 번째 이유로는 EC2 인스턴스 등 여러 AWS 서비스들을 사용하고자 할 때, VPC가 ``default VPC`` 로 설정되어 있는 경우가 있습니다. 자칫 엉뚱한 대역에 서비스를 배치하게 될 수도 있으므로 지워줍니다.

![](https://images.velog.io/images/dustjs159/post/94f8ccff-1825-45af-a7c1-f2b375fe7425/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-03-07%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2011.12.06.png)

(EC2 인스턴스를 생성하려고 하는데 VPC가 ``default VPC``로 설정되어 있음)

## 📌 Subnet

* 서브넷은 VPC를 하나의 작은 단위로 분할한 IP 주소 범위
  * VPC보다 작은 범위의 IP 주소 범위
* **Public Subnet** & **Private Subnet**
  * 외부 인터넷과의 연결 여부에 따라 Public / Private 서브넷을 구분
  * Public 서브넷 내 리소스들은 외부 인터넷과 연결
  * Private 서브넷 내 리소스들은 외부 인터넷과 차단
* 서브넷은 두 가용영역(AZ)에 각각 생성이 됨

## 📌 Routing Table

* 서브넷 내에서의 패킷 Allow / Deny 규칙

## 📌 Internet Gateway

## 📌 NAT Gateway

## 📌 Security Group & Network Access Control List(ACL)

<img width="595" alt="스크린샷 2021-08-23 오전 2 38 00" src="https://user-images.githubusercontent.com/57285121/130364617-cb599b6c-df73-424c-84ee-ea367c28a24d.png">
   
* 보안 그룹(Security Group)과 네트워크 ACL(Access Control List)은 VPC 내 서브넷과 인스턴스에 대한 인바운드/아웃바운드 트래픽의 허용 및 거부 규칙을 제어하는 가상의 **방화벽**역할을 합니다.
* 보안 그룹은 **인스턴스에 대한 접근 규칙**을 설정합니다. 인스턴스 하나당 최대 5개의 보안 그룹을 설정할 수 있습니다.
* 보안그룹은 인바운드/아웃바운드 트래픽에 대해 **허용할 규칙만 지정**할 수 있습니다.
* 네트워크 ACL은 **서브넷에 대한 접근 규칙**을 설정합니다. 서브넷 단위로 접근 규칙을 설정하기 때문에 인스턴스마다 개별적으로 접근 규칙을 설정할 필요가 없습니다.
* 인바운드/아웃바운드 규칙은 적용할 **프로토콜**과 **포트번호**단위로 접근 규칙을 설정합니다. 포트번호는 **Well-Known Port**를 사용합니다.
   
|항목|보안 그룹|네트워크 ACL|
|------|---|---|
|설정 범위|**인스턴스** 단위|**서브넷** 단위|
|트래픽 흐름 제어|Inbound All Deny, Outbound All Allow|Inbound, Outbound All Allow|
|규칙|접근 규칙 허용만 가능(모두 차단, 허용할 규칙 생성하여 허용)|접근 규칙 허용/거부 둘 다 가능(모두 허용, 차단할 규칙 생성하여 차단)|
|트래픽 허용 방식|**Stateful**|**Stateless**|
   
Well-Known Port
* SSH : 22
* HTTP : 80
* HTTPS : 443
* SMTP : 25(메일 송신)
* POP3 : 110(메일 수신)
* FTP : 20, 21
* DNS : 53

### Stateful / Stateless
* Stateful : 요청 정보를 저장하여 **인바운드 규칙에 따라 허용된 트래픽은 별도의 아웃바운드 규칙 없이도 인바운드 트래픽의 요청에 응답할 수 있습니다.**   
> * Ex) 인바운드 규칙에 http 80번 포트가 허용되어 있으면 아웃바운드 규칙 설정 없이도 요청에 응답할 수 있습니다.   
* Stateless : 요청 정보를 따로 저장하지 않기 때문에 응답하는 트래픽의 상태과 상관없이 인바운드/아웃바운드 규칙을 따릅니다. 허용되는 인바운드 트래픽에 대한 응답은 **인바운드 규칙에 상관없이 아웃바운드 규칙을 따릅니다.**   
> * Ex) 인바운드 규칙에 http 80번 포트가 허용되어 있더라도 아웃바운드 규칙에 http 80번 포트가 허용되어 있지 않으면 요청에 응답할 수 없습니다.


## 📌 Elastic IP

## 📌 VPC Endpoint
