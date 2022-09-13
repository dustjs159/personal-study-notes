💻 [AWS] AWS Transit Gateway
=============================
# 💡 AWS Transit Gateway (TGW)

* Transit Gateway VPC와 VPC 혹은 온프레미스와 VPC를 연결할 수 있는 라우터(허브)
* VPC간 연결에 있어서 1:1만 지원하던 VPC Peering과는 달리 중앙 집중형 방식으로 VPC들을 연결할 수 있음
    * 망 분리 환경 구성이 가능 

## 📌 Transit Gateway 주요 개념

* Attachment
    * TGW를 통해 통신에 참여하고 싶은 주체
    * VPC, VPN, Peering 등이 대상
    * Attach 유형이 VPC인 경우, TGW와 통신하고자 하는 대상(VPC & AZ & 서브넷)을 지정
* Route Table
    * TGW에 연결된 Attchment으로부터 들어온 트래픽의 다음 Hop을 결정(어디로 보낼 것인지) 
    * Association
        * TGW가 트래픽을 수신(Ingress)할 대상 → 어떤 Attachment로 부터 수신할 지
        * Attachment는 오직 하나의 Route Table에만 Association할 수 있음
    * Propagation
        * Attachment의 Route Table에 변경 사항이 있을 때 Attachment로부터 변경 사항을 전파받아 TGW의 Route Table에 적용
    * Routes
        * TGW가 트래픽을 송신(Egress)할 대상 → 다음 Hop은 어디인지
        * 유형은 Propagated, Static이 있음
* Prefix List 설정 가능

## 📌 Transit Gateway 구성 단계

* Cross Account 상황이라고 가정
    * 공유한 계정(A), 공유받은 계정(B)

1. TGW를 생성한 계정에서 RAM(Resource Access Manager)를 통해 TGW 장비를 공유
2. A, B 둘 다 Attachment를 생성
3. A에서 Route Table 생성
4. Route Table의 Association 등록
5. propagtions에서 routes를 생성하거나 routes에서 static으로 routes를 생성
6. A, B 계정에서 기존 VPC(Subnet)의 Route Table을 수정(TGW 방향으로 트래픽이 전달 될 수 있게) 