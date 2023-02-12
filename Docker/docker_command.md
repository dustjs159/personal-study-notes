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

## MacOS에서 docker 자동완성 설정하기
* 편리한 docker 커맨드 사용을 위해 `tab` 으로 커맨드 자동완성 기능 설정
* zshell 설정
    * `~/.zshrc` 파일 수정 (없으면 생성)
```vim
plugins=(
docker
docker-compose
)
```

* 변경 사항 적용
```bash
source ~/.zshrc
```
