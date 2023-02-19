💻 [Docker] Container
==================
## Container
* 컨테이너는 호스트 내에서 Docker Enigne 위에서 작동하는 격리된 app의 실행 단위
    * Docker는 이러한 컨테이너를 생성하는 도구.
* 컨테이너는 **이미지를 기반으로 실행된다.**

<img width="1145" alt="스크린샷 2023-02-05 오후 2 46 42" src="https://user-images.githubusercontent.com/57285121/216803895-561842ea-3267-41b5-953d-17ccdc873315.png">


## 빌드한 이미지로 컨테이너 실행하기

* 컨테이너 시작(Run)
    * `-d` : daemon (백그라운드 데몬)으로 실행
    * `--name {container name}` : 컨테이너 이름 지정
    * `-p {host-port}:{container-port}` : 매핑할 포트 지정
    * `--restart=always` : 서버 재시작 후 Docker 데몬까지 정상 작동 되어 있을 경우, 컨테이너도 자동 재시작 
```
docker run -d --restart=always --name {container name} {image} -p {host-port}:{container-port}
```
* 컨테이너 생성
```
docker craete {image}
```
* 컨테이너 시작(Start) - 특정 이미지로 실행되었던 컨테이너의 이미지에 대한 변경사항이 없을 때 사용. 백그라운드에서 실행됩니다.
```
docker start {container}
```
* 컨테이너 이름 변경
```
docker rename {old_container} {new_container}
```
* 컨테이너만 중지
    * 컨테이너 내 프로세스를 일시적으로 `stop`
```
docker pasue {container}
```
* 컨테이너 재시작
```
docker unpause {container}
```
* 컨테이너 종료
    * SIGTERM 시그널 전달
```
docker stop {container}
```
* 모든 컨테이너 종료
```
docker stop $(docker ps -a -q)
```
* 컨테이너 강제 종료
    * SIGKILL 시그널 전달
```
docker kill {container}
```
* 컨테이너 삭제(실행중이지 않을 때)
```
docker rm {container}
```
* 컨테이너 강제 종료 && 삭제 (SIGKILL 시그널 전달)
```
docker rm -f {container}
```
* 중지 상태인 컨테이너 삭제
```
docker container prune
```

* log 확인하기
```
docker logs {container}
docker logs -f {container} # Tailing
```

## docker run vs start 
* `docker run` 명령어로 컨테이너를 실행하면 포그라운드로 실행이 된다. 그런데 `docker start` 로 컨테이너를 실행하게 되면 백그라운드로 실행이 된다. 두 명령어의 default 실행 모드가 다르기 때문이다.
* `docker run` 은 default가 attached 모드(포그라운드)로 컨테이너가 실행되며 `docker start` 는 default로 detached 모드(백그라운드)로 실행이 된다.
* `docker run` 으로 백그라운드에서 컨테이너를 실행시키고자 한다면 `-d` 옵션(detached)을 사용한다.
    * `docker run -d ....`
* `docker start` 로 포그라운드에서 컨테이너를 실행시키고자 한다면 `-a` 옵션(attached)을 사용한다.
    * `docker start -a ....`
* 이미 실행중인 컨테이너에 직접 연결하고자 한다면...
    * `docker attach {container}`