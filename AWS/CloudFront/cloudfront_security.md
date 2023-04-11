💻 [AWS] CloudFront Security
==============================
## CloudFront에서의 보안

CloudFront를 보다 안전하게 사용하기

1. OAI(Origin Access Identity)
    * S3 버킷 내 오브젝트를 CloudFront를 통해서만 접근할 수 있도록 제한
    * S3 버킷 정책을 통해 CloudFront를 제외한 나머지 접근을 제한하여 사용자들의 버킷 직접 접근을 막음
2. OAC(Origin Access Control)
    * 기존 OAI의 새로운 버전. AWS에서 서명한 자체 자격 증명. OAC + Bucket Resource 기반 정책을 통해 버킷 접근을 제한할 수 있음
    * Origin Type이 Custom인 경우 사용 불가
3. Field Level Encryption
    * CloudFront ↔️ Origin 사이의 통신을 암호화
    * 공개키 암호화 방식으로 암호화
        * CloudFront에 Public Key가 있고, Origin에게 데이터 전송 시 Public Key로 암호화 하여 전송, Origin에서는 Private Key로 복호화
    * CloudFront가 Viewer와 HTTPS 통신을 지원하기에 CloudFront와 Origin간의 통신은 HTTP 통신을 하는 경우가 있는데, 이 때 CloudFront와 Origin간 거리가 멀 경우 탈취 가능성이 있기 때문에 암호화를 한다.
4. 국가 제한 기능

### CloudFront POP에 인증서 적용하기
![CloudFront](https://user-images.githubusercontent.com/57285121/180595009-6016e94c-8f7e-45aa-96bf-99d676772907.jpg)

* CloudFront에 ACM(AWS Certificate Manager)에서 발급받은 SSL/TLS 인증서를 적용하여 Origin의 웹 서버에서 따로 HTTPS를 적용하지 않고도 HTTPS를 적용할 수 있음
* 이 때 CloudFront에 적용할 인증서는 **버지니아 리전**에서 발급받은 인증서만 적용할 수 있다.

### CloudFront 앞단에 WAF 설정하기
* 외부의 비정상적인 행위를 탐지 및 차단하여 CloudFront를 보호  