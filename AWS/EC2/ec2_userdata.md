💻 [AWS] EC2 Userdata
=============
* Userdata : EC2 인스턴스가 생성될 때 사용할 Bootstrap Script
* 인스턴스를 실행할 때 필요한 소프트웨어 설치 자동화 가능
  * nginx나 mysql 등
* 패키지 업데이트, nginx 설치 및 시작하는 script를 미리 작성하여 인스턴스 내에서 실행할 작업 수행 가능
* User data에 입력한 Script는 Root 권한으로 실행되기에 따로 sudo 명령어를 작성할 필요 없음.

아래는 Ubuntu OS 인스턴스가 생성될 때 패키지 업데이트, nginx 설치, 웹 페이지 내용 변경, nginx 버전 숨기기(보안 권장 사항)를 진행하는 bootstrap script.

```bash
#!/bin/bash
apt update && apt upgrade -y
apt install nginx -y
echo "<h1> Hello nginx Web Server! Host : $(hostname)" > /var/www/html/index.nginx-debian.html
nginx_conf="/etc/nginx/nginx.conf"
uncommented_line="server_tokens off"
sed -i "s/# $uncommented_line/$uncommented_line/" $nginx_conf
systemctl restart nginx && systemctl enable nginx
```