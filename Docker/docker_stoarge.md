💻 [Docker] Storage
======================

# Docker의 이미지 파일은 어디에 위치?
* docker pull로 받은 이미지들은 어디에 저장될까?
* `docker info` 로 확인 가능하다.
    * Ubuntu 22.04 기준
```
docker info

...
...
Docker Root Dir: /var/lib/docker
...
...
```
* `Dockr Root Dir`에 `/var/lib/docker` 라고 지정되어 있는 것을 볼 수 있다.

```
root@demo:/var/lib/docker# ls -al
total 52
drwx--x--- 13 root root 4096 Jan 24 08:58 .
drwxr-xr-x 40 root root 4096 Jan 24 08:41 ..
drwx--x--x  4 root root 4096 Jan 24 08:41 buildkit
drwx--x---  3 root root 4096 Jan 24 14:08 containers
drwx------  3 root root 4096 Jan 24 08:41 image
drwxr-x---  3 root root 4096 Jan 24 08:41 network
drwx--x--- 12 root root 4096 Jan 24 14:08 overlay2
drwx------  4 root root 4096 Jan 24 08:41 plugins
drwx------  2 root root 4096 Jan 24 08:58 runtimes
drwx------  2 root root 4096 Jan 24 08:41 swarm
drwx------  2 root root 4096 Jan 24 09:16 tmp
drwx------  2 root root 4096 Jan 24 08:41 trust
drwx-----x  2 root root 4096 Jan 24 08:58 volumes
```
* `/var/lib/docker/containers` 디렉토리에 가보니, 현재 실행중인 컨테이너 ID와 같은 이름의 디렉토리를 찾을 수 있었다.
```
root@demo:/var/lib/docker/containers# ls -al
total 12
drwx--x---  3 root root 4096 Jan 24 14:08 .
drwx--x--- 13 root root 4096 Jan 24 08:58 ..
drwx--x---  4 root root 4096 Jan 24 14:46 ba62e7b30ed95a94d2cf22ba8127b622c7e882707718acbb0a8f6ebcf07e7908
root@demo:/var/lib/docker/containers# docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS     NAMES
ba62e7b30ed9   nginx     "/docker-entrypoint.…"   37 minutes ago   Up 36 minutes   80/tcp    nginx-demo
```

