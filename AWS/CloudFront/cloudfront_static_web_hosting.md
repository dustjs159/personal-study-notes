💻 [AWS] CloudFront + S3 Static Web Hosting
==========================
# CloudFront + S3 구조의 Static Web Application 배포하기
* CDN의 장점인 컨텐츠 전송 속도를 잘 활용하여 Static Web App을 배포해보자. 정적 컨텐츠에 보다 더 특화되어 있는 CloudFront + 정적 웹 페이지를 호스팅할 수 있는 S3의 조합은 아주 좋다.

## CloudFront + S3 구조의 장점
1. 빠른 속도 
2. 별도의 Auto Scaling 설정이 필요 없어 트래픽 대응에 수월
3. EC2 인스턴스 OS의 보안패치 및 EOL/EOS 걱정이 없음

## 사전에 알아두어야 할 CloudFront 주요 설정 옵션
* Origin 도메인 및 경로 설정
  * Origin 도메인을 S3 버킷으로 설정하고 경로를 설정하면 해당 경로의 폴더가 루트 폴더가 된다.
  * Origin 도메인의 버킷이 `example-test`, Origin 경로가 `/dev` 일 때 사용자가 CloudFront Distribution에 `index.html` 파일을 요청하면 `example-test/index.html`이 아닌 `example-test/dev/index.html`을 응답으로 반환
  * Origin을 Static 웹 페이지를 호스팅하는 버킷으로 지정하고자 하는 경우 S3 버킷의 Properties중 Static website hosting을 Enable한 후 주어지는 Bucket website endpoint으로 설정해줘야 한다. **(그냥 버킷 이름 X)**

<img width="765" alt="스크린샷 2022-10-26 오전 12 35 48" src="https://user-images.githubusercontent.com/57285121/197818319-a1c09fea-d639-4c5e-882a-2db1dec4c4c6.png">
<img width="628" alt="스크린샷 2022-10-26 오전 12 30 53" src="https://user-images.githubusercontent.com/57285121/197818401-a83d43c5-e086-4f70-9a32-657c85cd2239.png">


### 1. S3 버킷 생성
* 버킷을 생성한 후 Public Access Block을 해제하여 Public 접근이 가능하도록 한다.
* 버킷에 리소스 기반 정책을 적용한다.
    * 이 때 CDN POP만 접근(`GetObject`)가능하도록 설정했을 때 잘 안됐던걸로 기억하는데... (추가로 테스트 해봐야 함)
* S3 버킷의 Static Website hosting 기능을 `Enable` 한다. 
  * Index Document에 `index.html` 지정

### 2. CloudFront 배포(Distribution) 지점 만들기 (CDN POP)
* CloudFront 콘솔에서 `Create Distribution`
* Origin Domain을 입력할 때 S3 버킷의 웹 호스팅 엔드포인트를 설정

**웹 호스팅 엔드포인트가 아닌 S3 버킷 엔드포인트를 사용하면 여러 폴더를 나누어 렌더링 페이지 등을 띄우고자 할 때 CloudFront에서 설정한 Default Root Object (보통 index.html)가 여러 폴더 밑의 index.html을 찾지는 못한다.**

**Root 디렉토리 내의 `index.html` 은 찾지만 `/dev/index.html` 은 못 찾음... (Full Path를 입력하면 띄워지긴 한다. `example.com/dev/index.html` 를 입력한다면 정상적으로 띄워지기는 함) 특정 폴더 아래의 `index.html`을 찾기는 S3 버킷 Static Website hosting 설정을 할 때 지정하는 index document가 담당한다.**

**따라서 반드시 CloudFront + S3 구조의 정적 웹페이지를 구성할 때는 S3의 Static Website Hosting 기능을 활성화하고 index document를 지정한 뒤에 해당 엔드포인트를 CloudFront의 Origin 도메인으로 지정해야한다.**

* Default Root Object 지정 : `index.html`
* Alterdate Domain Name : 도메인 입력


* WAF, SSL/TLS 인증서 적용 등 옵션 사용

### 3. 빌드 결과물 S3에 파일 업로드 및 DNS 등록
* Route 53 Public Zone에 CloudFront Distribution Domain Name 등록.