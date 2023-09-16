💻 [AWS] ECS Cluster
=============================
# ECS Cluster
* Service / Task의 논리적인 그룹

## 생성 시 옵션
* Networking : 클러스터를 배치할 VPC, Subnet
* Infrastructure : 컨테이너를 배치할 인프라 정의
    * Fargate 유형 (Serverless)
    * EC2 유형
    * on-premise
* Container Insights : ECS 모니터링 활성화 여부
    * Metric, Log 자동 수집 가능

## pricing
* 비용 : 클러스터 자체에 대한 비용은 무료