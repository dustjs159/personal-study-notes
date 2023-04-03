💻 [AWS] AWS Transit Gateway
=============================
# 💡 AWS Transit Gateway (TGW)

* Transit Gateway VPC와 VPC 혹은 온프레미스와 VPC를 연결할 수 있는 L3 라우터(허브)
* VPC를 연결하는 방법 중 하나인 VPC Peering의 단점을 개선
* VPC Peering의 단점은 다음과 같다.
    * VPC간 전이성 Peering이 지원되지 않음(Non-Transitive). VPC간 Peering이 1:1만 지원된다. 
        * 따라서 1:1로 하나씩 연결해줘야 함.
    * 운영중인 VPC의 수가 점점 늘어날 수록 일일이 Peering 연결을 하는 것은 상당히 번거로운 일.
        * 즉, Peering의 수가 `n(n-1)/2` 개가 된다.
* 이러한 단점을 개선한 것이 Transit Gateway.
    * 연결 할 VPC의 수가 늘어날 수록 간편해진다. (다만 BGP에 대한 개념이 없으면 초기 구축에 있어서 다소 난이도가 있는 편.)
* 또한 VPC Peering에 비해 비용이 상당히 비싸므로 상황에 맞게 사용하는 것이 바람직.
    * 규모가 크지 않다면 VPC Peering을 사용하는 것이 더 저렴하고 편리하다.

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