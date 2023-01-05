💻 [AWS] AWS KMS
=============================
# 💡 AWS Key Managemet Service (KMS)

* 데이터 암복호화 및 전자 서명에 사용하는 Key를 생성 및 관리해주는 매니지드 서비스
* 생성한 Key는 내부적으로 HSM (Hardware Security Module)을 사용하여 안전하게 보관됨
* Key에 대한 접근은 보안상 민감한 부분이기 때문에 Key에 대한 모든 접근(암호화, 복호화 등)은 CloudTrail 에서 추적 

## 📌 KMS 주요 개념
KMS 서비스를 이해하기 위해서는 암호화에 대해 기본적인 지식이 필요합니다. 

* AES
* RSA
    * 2048
    * 4096

### AWS 관리형 Key
* AWS에서 관리하는 Key

### Custom Managed Key
* 사용자가 직접 만들어 사용할 수 있는 Key.