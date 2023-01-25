💻 [Docker] Command
======================

# Docker 커맨드 모음
* Docker 정보 확인
```
docker info
```
* Docker Hub에서 특정 이미지 검색
    * 웹 URL : https://hub.docker.com/
```
docker search {image}
```
* 서버 내 저장된 이미지 확인
```
docker images
```
* 이미지 상세 정보 확인
```
docker inspect {image}
```
* 이미지 pull
    * version은 선택. 특정 버전을 지정하지 않을 경우 생략한다. 그러면 최신 버전(latest)을 pull
```
docker pull {iamge}:{version}
```
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
* 컨테이너 시작(Start)
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
```


