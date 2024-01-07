Terraform Resource Management
=====================

### resource : 생성할 인프라 자원 명시
```
resource "<PROVIDER>_<TYPE>" "<NAME>" {
    [CONFIG...]
}
```
* PROVIDER : 클라우드 공급 업체
* TYPE : 리소스 유형
* NAME : 리소스를 참조할 수 있는 식별자
* CONFIG : 리소스를 생성할 때 필요한 설정값
    * 하나 이상의 argument로 구성됨

### attribute 참조하기
* resource 블록에서 선언한 리소스 이름의 attribute를 참조하여 새로운 resource 블록 생성이 가능