💻 [AWS] IAM Credentials
=================
* IAM Credential - Access Key & Secret Key
    * CLI, SDK등의 AWS API를 호출하기 위해 필요한 정보. 반드시 유출되지 않도록 해야한다. (매우 중요)
    * User당 2개까지 생성할 수 있음

## Access Key, Secret Key 셋업하기
* `aws configure` 명령어 사용
    * AccessKey, Secret Key, Region 입력
    * 입력 후에 `~/.aws/credentials` 파일에 해당 입력값이 저장됨
    * MFA or Assume Role 적용을 위해서는 `~/.aws/config` 파일에 별도의 설정값 입력 필요

`~/.aws/credentials` 파일 구성
```vim
[default]
aws_access_key_id=*****
aws_secret_access_key=***** 
```

`~/.aws/config` 파일 구성
```vim
[default]
region=ap-northeast-2
mfa_serial=[MFA ARN]
role_arn=[Role ARN]
```

## Leapp 활용하기
* AWS SDK를 사용하여 서비스 개발을 할 때 장기(AccessKey & SecretKey) 혹은 임시(STS)자격 증명이 반드시 필요하다. 이 때 `Leapp` 이라는 프로그램을 통해 자격 증명 설정을 편하게 하는 방법을 소개한다.
    * 다운로드 페이지 : https://www.leapp.cloud/
    * Mac 이외의 환경에서는 사용해보지 않았다...

1. 장기 자격 증명 사용하기
- 개인 사용자가 AccessKey, SecretKey 정보를 기억하고 있다고 가정한다.
- 앱 설치 후 상단의 `"+"` 버튼 클릭
- Cloud Provider : AWS
- Access Method 에서 "AWS IAM User"  선택
- ..(작성 예정)

2. 임시 자격 증명 사용하기
