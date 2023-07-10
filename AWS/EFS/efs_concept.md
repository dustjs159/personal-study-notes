💻 [AWS] Amazon EFS
===================

* Amazon EFS(Elastic File System) : 인스턴스에 연결하여 사용할 수 있는 **파일 스토리지**
    * 자동 확장 가능한 네트워크 파일 시스템(NFS)
        * 용량을 정해두고 사용하는것이 아니라 사용한 만큼 GB 단위로 요금이 청구된다.
    * Security Group으로 접근 제어
    * Linux 기반 인스턴스만 사용 가능함. 윈도우 불가
    * VPC Level 서비스
    * 성능모드 / 처리량모드