AWS 2-Tier Architecture
====================================
## Summary
- Last Updated : 21.09.03 Fri   
- Updated by : YEONSUN YOON
-----------------------------------

# 2-Tier Architecture
* 응용 소프트웨어를 통해 결과를 클라이언트에게 출력하고 클라이언트에게 출력할 데이터들이 그 데이터들이 서버에 저장되는 형태   
> * Ex) 사용자가 구글 크롬(웹 브라우저 소프트웨어)으로 접속하여 정보를 검색하면 구글 웹 서버에 저장된 데이터들을 출력해줌   
* **Client-Server(C/S)** 형태
   
<img width="679" alt="스크린샷 2021-09-04 오후 3 39 51" src="https://user-images.githubusercontent.com/57285121/132085424-690aca39-7809-4c29-ac4d-dc7c5eef1fc9.png">
      
> * **단순한 결과 출력은 클라이언트 측에서 처리**하고 그 외의 요청은 서버에 전달하며 서버는 **받은 요청에 대해 처리를 진행**   
> * 단일 고성능 서버로 모든 클라이언트의 요청을 처리하는 통합형 아키텍처보다 낮은 성능의 서버를 여러 대 배치하여 비용을 낮출 수 있다는 장점   
> * 하지만 고가용성에 대한 고려와 클라이언트측에서 꾸준한 소프트웨어 업데이트를 필요로 한다는 단점이 존재   
 
# 아키텍처 구성
* Web Server : Apache
* Web Application Server(WAS) : Tomcat
* Apache <-> Python
* Apache <-> Tomcat

## Network 구성
1. VPC 생성   
> * IPv4 CIDR : `10.3.0.0/24` -> 생성할 수 있는 VPC의 IP 범위는 사설 IP 대역 + prefix `/16` ~ `/28`   
> * 태그 - 키 : `Name`, 값 : `yys_vpc1`
   
<img width="757" alt="스크린샷 2021-09-04 오후 4 04 11" src="https://user-images.githubusercontent.com/57285121/132085961-b7672e5c-71d4-4bcd-bf3b-210be1bc4fea.png">
   
2. Subnet 생성
* Public / Private Subnet
* Routing Table
* IGW
* NAT Gateway : Public Subnet에 위치하고 Private Subnet이 외부랑 연결되는데 사용

## Server 구성
* Amazon EBS
* ELB

## 
