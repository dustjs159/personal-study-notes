💻 [AWS] S3 Bucket Policy
==================
* S3 버킷에 접근하기 위한 자격 증명 기반 정책(Identity-based policy)
* S3 버킷에 대한 접근 제어를 위해 리소스 기반 정책(Resource-based policy)부여 가능


## Principal에 정책 부여할 때

* S3에 접근하고자 하는 Principal에 Policy를 Custom하여 Attach할 때 유의점
```json
1. "Action": "ListAllMyBuckets"
2. "Action": "ListBucket"
```
* 위 1번은 계정 내 존재하는 버킷의 리스트를 조회하는 Action
  * `ls bucket` 
* 위 2번은 버킷 내 존재하는 객체(Object)의 리스트를 조회하는 Action
  * `ls object` 
* 따라서, 정책을 할당할 때 `ListAllMyBuckets`으로 버킷 리스트를 조회할 수 있도록 하고 `ListBucket` + 특정 bucket name을 통해 특정 버킷의 object들만 확인할 수 있도록 할당
  * `ListAllMyBuckets` 를 허용하지 않으면 `ListBucket` 를 모든 버킷에 허용해도 버킷 리스트 자체가 조회가 되지 않기 때문에 아무것도 볼 수 없다.
