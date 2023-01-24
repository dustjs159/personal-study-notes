💻 [Docker] Install
==================
# 💡 Docker 설치 및 사용법
* Docker 설치 - Linux OS
* Docker Hub에 이미지 업로드 & 다운로드
* Docker Command

## 📌 Docker 설치
* Ubuntu 22.04 LTS 에서 진행
  * URL : https://docs.docker.com/engine/install/ubuntu/

1. 필요한 패키지 설치
    - 그 전에 이미 설치되어 있는 건지 확인
```bash
apt list --installed | grep -P "gnupg|curl|certificate|lsb-release"
```
- 설치가 안되어 있다면 설치

```bash
apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```
2. Docker GPG Key 설정
    - 설치한 패키지가 검증된 패키지인지 검사하는 용도라고 합니다. 자세한건 저도 잘..
```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```
```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

3. Docker 엔진(CE, Community Edition), CLI, containerd 패키지 설치
```bash
apt-get update
apt-get install docker-ce docker-ce-cli containerd.io
```

4. 설치 확인 (Run Test)
```bash
docker run hello-world
```

5. (optional) 일반 사용자에게 docker 실행 권한 부여하기
* docker는 최초에 root 계정에서 실행되기 때문에 일반 사용자에서 실행하게 되면 Access Denied 발생하기에 실행 권한 설정해줘야함.
```bash
usermod -aG docker app1
cat /etc/group # docker group에 app 계정이 포함되어 있는지 확인.
```
* 이후 docker 재시작.
