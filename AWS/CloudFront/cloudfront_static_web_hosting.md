💻 [AWS] CloudFront + S3
===============

## CloudFront + S3 조합으로 정적 웹 페이지 호스팅하기
* 정적 컨텐츠에 보다 더 특화되어 있는 CloudFront + 정적 웹 페이지를 호스팅할 수 있는 S3의 조합은 아주 좋다.
* 빌드 결과물에 따라 조금 씩 다를 수 있다는 점...
* 웹 앱의 빌드 결과물은 `index.html` 파일이라 가정한다.

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
    * 이거도 설정 안하면 잘 안되더라고.. 마찬가지로 추가 테스트 좀 더 해봐야 함.
* WAF, SSL/TLS 인증서 적용 등 옵션 사용

### 3. 빌드 결과물 S3에 파일 업로드 및 DNS 등록
* Route 53 Public Zone에 CloudFront Distribution Domain Name 등록.