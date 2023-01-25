💻 [Docker] Demo - Nginx Install
===============================
# 💡 Docker Demo - Nginx 웹서버 실행하기
* Docker Hub에서 최신 버전의 Nginx 이미지를 받아 컨테이너 실행하기
* EC2 인스턴스(OS : Ubuntu 22.04 ARM)에서 진행
* 진행 전, Docker가 정상적으로 실행중이라고 가정.

### 1. pull할 이미지 검색
```
app@demo:~$ docker search nginx
NAME                                              DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
nginx                                             Official build of Nginx.                        17972     [OK]
```
* 최상단에 Official 이미지가 있는걸 확인할 수 있다. Stars도 가장 많다.
    * docker hub에서 nginx로 검색해도 찾을 수 있다.

<img width="1202" alt="스크린샷 2023-01-24 오후 6 31 16" src="https://user-images.githubusercontent.com/57285121/214256817-53d62269-ddc6-48e9-87bd-65a378cfbd72.png">


### 2. 이미지 Pull
```bash
docker pull nginx
docker pull nginx:{version} # 특정 버전
```
* 별도의 버전을 명시하지 않으면 latest 태그가 붙은 최신 버전의 이미지를 pull
* 특정 버전을 명시할 경우 해당 버전을 pull
* 확인
```bash
app@demo:~$ docker images
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
nginx         latest    d8906c7d4c44   13 days ago     135MB
```

### 3. pull한 이미지를 바탕으로 컨테이너를 실행
* pull한 이미지를 실행할 떄 컨테이너 단위로 실행이 됨
* 그 과정에서 **포트 매핑, 컨테이너에서 실행할 이미지, 컨테이너 이름** 등을 지정해줘야한다.
    * `-d` : 백그라운드 실행(daemon으로 실행하고자 할 때)
    * `-p` : port 매핑
        * 호스트에서 LISTEN하는 포트와 컨테이너가 LISTEN하는 포트번호를 매핑
    * `--name` : 컨테이너 이름 지정할 때 사용
```bash
docker run -d --name nginx-demo -p 80:80 nginx
```
* 확인
```
app@demo:~$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS                               NAMES
34fd5c872f31   nginx     "/docker-entrypoint.…"   4 seconds ago   Up 3 seconds   0.0.0.0:80->80/tcp, :::80->80/tcp   nginx-demo
```
* 실제 브라우저에서 확인해보자.
    * EC2에 Elastic IP, 그리고 Security Group에서 내 IP만 허용하여 확인했다.

<img width="1628" alt="스크린샷 2023-01-24 오후 6 47 01" src="https://user-images.githubusercontent.com/57285121/214260298-a2cd4d59-9654-430b-beb5-75d4fc32f9cf.png">

아주 잘 나온다.

### 4. 컨테이너 중지, 재시작, 삭제
* 컨테이너만 중지
    * 컨테이너 내 프로세스를 일시적으로 `stop`
```
docker pause {container}
```
* 컨테이너 재시작
```
docker unpause {container}
```
* 컨테이너 삭제
```
docker rm -f {container}
```
### 번외
* `docker run`이 아닌 `docker create` 로 컨테이너를 실행시켜보자.
```
docker rm -f nginx-demo # 기존에 실행중인 컨테이너 삭제

docker create nginx # pull했던 이미지로 컨테이너 생성
```
* 여기까지 진행한 후 `docker ps -a` 로 컨테이너를 확인해보면, 이름이 이상하게 되어있다. 이거를 이전과 동일하게 `nginx-demo` 로 변경해준다.
```
docker rename {old_container} nginx-demo
```
* 그리고 시작
```
docker start nginx-demo
```
