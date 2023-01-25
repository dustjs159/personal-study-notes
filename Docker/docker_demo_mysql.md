💻 [Docker] Demo - MySQL Install
===============================
# 💡 Docker Demo - MySQL 실행하기
* Docker Hub에서 최신 버전의 MySQL 이미지를 받아 컨테이너 실행하기
* EC2 인스턴스(OS : Ubuntu 22.04 ARM)에서 진행
* 진행 전, Docker가 정상적으로 실행중이라고 가정.

### 1. pull할 이미지 검색
```
app@demo:~/docker-mysql$ docker search mysql
NAME                            DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
mysql                           MySQL is a widely used, open-source relation…   13724     [OK]
mariadb                         MariaDB Server is a high performing open sou…   5236      [OK]
```
* 최상단에 mysql 이미지가 있는걸 확인할 수 있다. Stars도 가장 많다.
    * docker hub에서 mysql로 검색해도 찾을 수 있다.

![스크린샷 2023-01-26 오전 12 30 06](https://user-images.githubusercontent.com/57285121/214604888-182dd968-e885-4eab-800f-2620a548f463.png)


### 2. 이미지 Pull
```bash
docker pull mysql
docker pull mysql:{version} # 특정 버전
```
* 별도의 버전을 명시하지 않으면 latest 태그가 붙은 최신 버전의 이미지를 pull
* 특정 버전을 명시할 경우 해당 버전을 pull
* 확인
```bash
app@demo:~$ docker images
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
mysql         latest    be430b9d80e5   7 days ago      527MB
```

### 3. pull한 이미지를 바탕으로 컨테이너를 실행
* pull한 이미지를 실행할 떄 컨테이너 단위로 실행이 됨
* 그 과정에서 **포트 매핑, 컨테이너에서 실행할 이미지, 컨테이너 이름** 등을 지정해줘야한다.
    * `-d` : 백그라운드 실행(daemon으로 실행하고자 할 때)
    * `-p` : port 매핑
        * 호스트에서 LISTEN하는 포트와 컨테이너가 LISTEN하는 포트번호를 매핑
    * `--name` : 컨테이너 이름 지정할 때 사용
    * `--restart=` : 재시작 옵션
        * `always` : 서버 재시작 후 docker 데몬이 정상 작동중이라면 언제든 컨테이너 자동 재시작
    * `-e` : mysql의 환경 변수를 지정합니다. (필수)
        * `MYSQL_ROOT_PASSWORD` : root 계정 비밀번호 설정
        * `MYSQL_ALLOW_EMPTY_PASSWORD` : `yes` 로 설정할 경우 root 계정 비밀번호 설정 없이 진행(비권장)
        * `MYSQL_RANDOM_ROOT_PASSWORD` : root 계정 비밀번호 랜덤 설정
```bash
#!/bin/bash

# Bash Script로 작성하여 실행
docker run -d --restart=always --name mysql-demo -e MYSQL_ROOT_PASSWORD=1q2w3e4r! -p 3306:3306 mysql
```
* 확인
```
app@demo:~$ docker ps -a
app@demo:~/docker-mysql$ docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                                                  NAMES
a0ed49b48d61   mysql     "docker-entrypoint.s…"   21 minutes ago   Up 21 minutes   0.0.0.0:3306->3306/tcp, :::3306->3306/tcp, 33060/tcp   mysql-demo
```
* 실제로 DB에 접속해보자.
```bash
docker exec -it mysql-demo bash

bash-4.4# mysql -u root -p
Enter password: # 설정한 password 입력

Welcome to the MySQL monitor. ....
....

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
```
잘 나온 모습.

