💻 [AWS] EC2 AMI
===================  

# 인스턴스의 이미지
![](https://images.velog.io/images/dustjs159/post/c7223c11-14b1-4ee6-8f75-af02079aaa05/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-01-09%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2011.02.18.png)

* AMI(Amazon Machine Image) : 인스턴스를 생성하기 위해 필요한 운영체제와 그 외 필요한 소프트웨어들(웹 서버 Nginx 등)이 설치된 이미지
* AWS에서 제공하는 AMI를 커스터마이징하여 동일한 구성의 여러 인스턴스를 찍어내듯 생성 가능(필요한 소프트웨어를 인스턴스 생성할 때마다 설치하지 않아도 됨)
* EC2 생성 시 선택할 수 있는 AMI 종류 
  * Linux : Amazon Linux2, Red Hat Enterprise Linux, Ubuntu, SUSE Linux 등
  * Windows : MS Windows Server
* 이미 만들어져있는 AMI 외에 개인이 직접 제작하여 Marketplace에서 배포도 가능하며 이 경우에는 AMI가 안전하지 않을 수도 있기 때문에 배포자를 잘 확인하고 사용
* 계정 간 공유 가능
* 마스터 이미지를 만들어 두고 사용하는 방법 이용
  * 보안 패치 및 필요한 소프트웨어 설치