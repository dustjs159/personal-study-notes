💻 Docker
==================
# 💡 Docker 개념
 
* 설치해야 할 서버의 수가 많지 않을 경우에는 직접 수작업으로 설치해도 큰 문제가 없지만, 설치해야 할 서버의 수가 수백, 수천대일 경우에는 수작업으로 설치하기 어려움
* Docker는 컨테이너라는 단위에 서버 운영에 필요한 구성품을 담아 배포 및 관리하는 리눅스 OS 기반의 Tool

## 📌 컨테이너(Container)

* Docker는 **컨테이너 기반의 오픈소스 가상화 플랫폼** 
  * 컨테이너 : 호스트 내 격리된 각각의 실행 환경
  * Docker는 컨테이너라는 논리적 단위에 설치하고자 하는 서버의 구성(lib, bin 등)을 담아 배포 및 관리를 수월하게 해줌
  * 컨테이너 내 APP들은 논리적으로 격리된 환경에서 실행

### ✔️ 컨테이너 가상화 기술
* 컨테이너는 일종의 **가상화** 기술
* VMware나 VirtualBox에서 사용하던 가상화 방식은 호스트 OS 위에 게스트 OS 전체를 가상화하는 방식

![스크린샷 2022-03-29 오후 5 21 23](https://user-images.githubusercontent.com/57285121/160566837-0a9a0178-ff2a-435d-b9c2-bed283c9c6c9.png)

* 기존의 가상화 방식에서 게스트 OS는 호스트 OS의 모든 하드웨어 자원을 공유하기 때문에 무겁고 느리다는 단점
* 이러한 단점을 극복하기 위해 호스트 OS 위에 게스트 OS를 설치하는 것이 아닌 Docker 엔진을 설치하고 그 위에서 App, Bin 파일 등을 실행
* VM 보다 훨씬 가볍고 빠름


## 📌 이미지(Image)

* 이미지는 컨테이너 실행에 필요한 파일과 설정값(App, Config)을 포함

![스크린샷 2022-03-29 오후 5 55 56](https://user-images.githubusercontent.com/57285121/160574048-9e59cac1-84a7-424e-b755-a24f0741011a.png)

* 같은 이미지에서 여러 컨테이너 생성 가능
* 컨테이너가 삭제되거나 변경되어도 이미지는 그대로
* 만들어 놓은 이미지를 다운받고 컨테이너를 생성하고 실행하면 됨
* 도커 이미지는 Docker Hub에 등록하거나 Docker Registry 저장소를 만들어 직접 관리 가능

# 💡 Docker 사용법

* Docker 설치 - Linux OS
* Docker Hub에 이미지 업로드 & 다운로드
* Docker Command

## 📌 Docker 설치
* Ubuntu 20.04 LTS 에서 진행
  * URL : https://docs.docker.com/engine/install/ubuntu/

Repository Set up
```bash
 $ sudo apt-get update
 
 $ sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```
Docker GPG Key Add
```bash
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```
Repository Status set ``Stable``
```bash
$ echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
Docker Engine Install
```bash
$ sudo apt-get update
$ sudo apt-get install docker-ce docker-ce-cli containerd.io
```
Check Docker Engine Version List
```bash
$ apt-cache madison docker-ce
```
Install Specific Version
```bash
$ sudo apt-get install docker-ce=<VERSION_STRING> docker-ce-cli=<VERSION_STRING> containerd.io
```
Run Test
```bash
$ sudo docker run hello-world
```

## 📌 Docker Hub 사용법

* Docker Hub에 이미지 업로드 & 다운로드
* Docker Hub 가입
  * https://hub.docker.com
* Repository 생성

## 📌 Docker Command

* ``$ docker pull  # Docker 이미지 가져오기 + Build까지 수행``
* ``$ docker push  # Docker 이미지 업로드``
* ``$ docker images # 갖고 있는 이미지 확인``
* ``$ docker run    # pull로 가져온 이미지(Build까지 다 된)를 컨테이너로 만들어 실행``
* ``$ docker ps     # 실행중인 컨테이너 확인``  
