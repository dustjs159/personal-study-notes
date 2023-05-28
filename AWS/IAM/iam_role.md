💻 [AWS] IAM Role
=================

* IAM Role
    * user가 아닌 principal에 대한 권한.
        * EC2, Lamdba Function, RDS 등등
* Role은 **임시 자격 증명**이다.

# Role 생성시 Trust Principal에 대해서
* EC2에서 특정 서비스에 접근하기 위한 Role을 생성하는 과정에서 다음과 같은 정책이 적용되는 것을 확인할 수 있다.
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "sts:AssumeRole"
            ],
            "Principal": {
                "Service": [
                    "ec2.amazonaws.com"
                ]
            }
        }
    ]
}
```

이 정책이 무엇인가 하는 생각이 들었는데 일반 유저가 특정 서비스에 접근할 때와 EC2에서 Role 기반으로 다른 서비스에 접근하는 방식이 다르다는 것을 인지하면 생각보다 간단한 해답이였다.

* 일반 사용자의 AccessKey, Secret Key 를 사용한 접근 : 장기 자격 증명
* EC2 인스턴스의 Role을 활용한 접근 : 임시 자격 증명

위 정책은 임시 자격 증명을 사용하기 위한 `sts` 서비스의 `AssumeRole` action을 ec2 서비스 주체가 사용할 수 있도록 설정하는 것이다. 즉 임시 자격 증명인 Role 기반으로 다른 서비스에 접근할 수 있게 되는 것.

인스턴스 내에서 일반 사용자의 AccessKey, SecretKey를 저장하고 특정 서비스를 이용하는 것도 가능한 방법이나 이는 바람직하지 못한 방법이다. 인스턴스가 사용중인 Key를 소유한 일반 사용자를 삭제하게 되면 즉시 서비스 장애가 발생할 수도 있고 Key 유출이 될 수도 있으므로 일반 사용자의 Key를 사용하여 서비스에 접근하는 장기 자격 증명이 아닌 Role 기반의 임시 자격 증명을 통해 서비스 접근 권한을 부여하도록 한다.