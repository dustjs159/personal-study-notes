💻 [Docker] Container
==================
## Container
* 컨테이너는 호스트 내에서 Docker Enigne 위에서 작동하는 격리된 app의 실행 단위
    * Docker는 이러한 컨테이너를 생성하는 도구.
* 컨테이너는 **이미지를 기반으로 실행된다.**

<img width="1145" alt="스크린샷 2023-02-05 오후 2 46 42" src="https://user-images.githubusercontent.com/57285121/216803895-561842ea-3267-41b5-953d-17ccdc873315.png">


## 빌드한 이미지로 컨테이너 실행하기

* 컨테이너 시작(Run)

`docker run --help` 명령어로 옵션을 확인할 수 있다. 
```
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```
주요한 옵션(자주 쓰는 것들)
 * `-d` : detached 모드로 실행(백그라운드)
 * `--name {container name}` : 컨테이너 이름 지정
 * `-p {host-port}:{container-port}` : 매핑할 포트 지정(publisher)
 * `--restart=always` : 서버 재시작 후 Docker 데몬까지 정상 작동 되어 있을 경우, 컨테이너도 자동 재시작
 * `--rm` : 컨테이너가 미사용 상태(`Stop`)가 될 경우 자동으로 컨테이너 삭제되도록 설정
```
docker run -d --rm --restart=always --name {container name} {image} -p {host-port}:{container-port}
```

## docker run vs start 
* `docker run` 명령어로 컨테이너를 실행하면 포그라운드로 실행이 된다. 그런데 `docker start` 로 컨테이너를 실행하게 되면 백그라운드로 실행이 된다. 두 명령어의 default 실행 모드가 다르기 때문이다.
* `docker run` 은 default가 attached 모드(foreground)로 컨테이너가 실행되며 `docker start` 는 default로 detached 모드(background)로 실행이 된다.
* `docker run` 으로 background에서 컨테이너를 실행시키고자 한다면 `-d` 옵션(detached)을 사용한다.
    * `docker run -d ....`
* `docker start` 로 foreground에서 컨테이너를 실행시키고자 한다면 `-a` 옵션(attached)을 사용한다.
    * `docker start -a ....`
* 이미 실행중인 컨테이너에 직접 연결하고자 한다면...
    * `docker attach {container}`

## 컨테이너 내부에 진입하기 - Interactive 모드
* `-i` 옵션을 통해 컨테이너의 내부에 진입하여 커맨드 입력이 가능 (interactive)
    * `STDIN` 상태 유지
* `-t` 옵션을 통해 커맨드를 입력할 터미널을 띄움 (tty)
* 즉 컨테이너 내부에 명령어를 전달하고자 할 때 `-i` 옵션을 통해 컨테이너가 STDIN으로 명령어를 입력 받을 준비하고 `-t` 옵션으로 입력 받을 터미널을 띄운다.
    * 합쳐서 `-it`로 많이 사용함
    * 근데 이러한 방식으로 컨테이너를 실행하고 특정 값을 입력받는 경우 한번만 입력값을 받고 컨테이너가 중지된다... 그리고 다시 띄우기 위해 `docker start` 를 하게 되면 default 실행 모드(detached)로 실행된다.(아무것도 변화가 없을 듯)
    * 그래서 `-a` 옵션으로 attached 모드로 실행하니 한 번의 입력값만을 받고 더 이상 입력 값을 받지 않는 현상이 있었는데 이는 `-i` 옵션이 없어서(= STDIN으로 받을 준비가 안되어 있어서) 한 번 받고 끝난 경우다. 함께 사용하면 입력값을 받을 수 있다.
        * `docker start -i -a {container}`

### 컨테이너 관련 command
```bash
# 컨테이너 실행
docker run {image} # 실행 모드 : attached (default) 

# 컨테이너 시작(특정 이미지로 실행되었던 컨테이너의 이미지에 대한 변경사항이 없을 때 사용)
docker start {container} # 실행 모드 : detached (default)

# 컨테이너 중지
docker stop {container} # SIGTERM

# 미사용 컨테이너 삭제
docker container prune

# 컨테이너 삭제
docker rm {container} # SIGKILL

# 컨테이너 강제 종료 && 삭제
docker rm -f {container}

# 파일 복사 
docker cp {local file path} {container}:{container file path} # local -> container
docker cp {container}:{container file path} {local file path}  # container -> local

# 컨테이너 로그 확인
docker logs {container}
docker logs -f {container} # Tailing

# 컨테이너 생성
docker create {image}

# 컨테이너 이름(Alias) 바꾸기
docker rename {old_container} {new_container}
```