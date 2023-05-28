💻 [AWS] IAM Credentials
=================
* IAM Credential - Access Key & Secret Key
    * CLI, SDK등의 AWS API를 호출하기 위해 필요한 정보. 반드시 유출되지 않도록 해야한다. (매우 중요)
    * User당 2개까지 생성할 수 있음

# Access Key, Secret Key 셋업하기
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
