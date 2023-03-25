💻 [Docker] Image
==================
## Image
* 이미지는 컨테이너 실행에 필요한 파일을 포함
    * 컨테이너 실행에 필요한 파일 : 코드와 코드 실행에 필요한 도구

<img width="1145" alt="스크린샷 2023-02-05 오후 2 46 42" src="https://user-images.githubusercontent.com/57285121/216803895-561842ea-3267-41b5-953d-17ccdc873315.png">

* 하나의 컨테이너를 실행하기 위해서는 이미지가 필요하다.
    * 하나의 이미지에서 여러 컨테이너 생성이 가능
    * 컨테이너가 삭제되거나 변경되어도 이미지는 그대로 보존이 가능
* 만들어 놓은 이미지를 다운받고 컨테이너를 생성하고 실행하면 됨
* 일반적으로 이미 만들어져 있는 이미지를 사용하거나(보통 docker hub에서 가져옴) 직접 이미지를 커스텀하여 사용한다.
    * docker hub : https://hub.docker.com/

## Image Build를 위한 Dockerfile
* **Dockerfile : 컨테이너에서 실행할 이미지를 빌드하기 위한 스크립트**
    * 베이스 이미지 + application 코드 + 필요한 라이브러리 or 패키지 설치 커맨드 등 컨테이너에서 실행할 이미지를 빌드하기 위해 필요한 스크립트 파일
    * 해당 프로젝트 폴더에서 `Dockerfile` 이라는 이름의 파일을 생성.

예시
```vim
FROM node

WORKDIR /app

COPY . /app

RUN npm install

EXPOSE 80

CMD ["node", "server.js"]
```

* `FROM` : docker hub or local의 base image 지정
    * local에 저장된 이미지가 있다면 local의 이미지를 가져오고 없으면 docker hub에서 가져옴
* `WORKDIR` : 컨테이너 내부에서 수행할 작업들을 진행할 경로. 이후 모든 작업은 해당 디렉토리에서 진행됨
* `COPY` : 컨테이너 외부(local)의 어떤 파일을 컨테이너 내부로 복사할 것인지 지정
    * `COPY {local file system} {container file system}`
        * 첫 번째는 로컬 호스트의 파일 경로, 두 번째는 컨테이너의 파일 시스템 경로. (절대 경로, 상대 경로 둘 다 작성 가능하다)
        * 컨테이너 파일 시스템 경로에 해당 디렉토리가 존재하지 않는다면 따로 생성하게 됨
* `RUN` : 이미지를 빌드할 때 필요한 커맨드를 작성
    * `RUN` 커맨드는 **컨테이너를 시작할 때 필요한 커맨드가 아닌 이미지 빌드를 위해 필요한 커맨드를 지정**
    * 이미지 빌드하는 측면과 컨테이너를 실행하는 측면에서 필요한 것이 다르기 때문
* `EXPOSE` : container가 listen 중인 포트 명시
    * 명시적으로 컨텍스트 공유 목적으로만 사용된다. 실질적으로 작성하지 않아도 되긴 하지만 문서화 목적에 있어서 작성하는 것이 좋다.
    * 따라서 실질적으로 `docker run -p 3000:80` 과 같이 publish(`-p` 옵션)할 포트를 지정해야 한다.
* `CMD` : 컨테이너를 실행할 때 필요한 커맨드를 작성
    * `RUN` 커맨드와의 차이점 - `CMD` 커맨드는 **빌드한 이미지로 컨테이너를 시작하는 시점에 필요한 커맨드를 지정**
    * **array 형태로 작성!**

## Dockerfile로 이미지 빌드
* Dockerfile이 위치한 현재 경로에서
```bash
docker build . # Dockerfile을 알아서 읽는다.
docker build -t {tag} . # 이미지에 태그 붙이기
```
* 생성된 이미지 확인
```bash
docker images
```

## 코드의 변경사항이 있을 때?
* 특정 이미지를 기반으로 가동중인 컨테이너에 코드 변경사항이 있을 때는 이미지를 다시 빌드하여 실행해야 한다.
* 현재 실행중인 컨테이너의 파일시스템에는 이전 버전의 이미지의 코드가 포함되어 가동중이기 때문에, 해당 코드가 변경된 이미지를 빌드하여 해당 컨테이너의 파일시스템에 포함시켜야 변경 사항이 반영된다.

## 이미지 레이어(Layer)
* 코드의 작은 변경 사항이 발생했을 때, 이미지를 빌드함에 있어서 처음부터 모든 것을 빌드하는 것은 비효율적
* Dockerfile을 통해 새 이미지를 빌드할 때 변경사항이 없는 부분은 내부 자체 **Cache** 를 사용하여 변한 부분만 반영에 대해서만 빠르게 빌드할 수 있다.
* 이것을 이미지 **레이어(Layer)** 라고 하는데. 아래 사진을 보자.

<img width="1450" alt="스크린샷 2023-02-12 오후 11 24 50" src="https://user-images.githubusercontent.com/57285121/218316827-fb2f061e-06a9-45ff-918a-4c841a7fe032.png">

* 컨테이너 실행을 위해 처음 빌드할 때는 아무런 캐시 정보가 없기 때문에 모든 Dockerfile의 명령어를 전부 수행한다. 
* 빌드된 이미지(tag : v1.0)로 컨테이너가 가동중이라고 가정하자. 이 때 코드에 변경사항이 생겨 새로 이미지를 빌드(v1.1)하게 되면 기존에 이미지(v1.0)위에 새 이미지(v1.1)가 빌드된다.
    * 모든 이미지는 **Read-Only.**
    * 기존 이미지(v1.0)는 내용 변경이 불가하며 캐싱 목적의 base layer 이미지가 되는 것!
    * 그리고 새로 빌드된 이미지(v1.1)은 컨테이너가 실행할 수 있는 이미지가 되어 컨테이너가 실행된다.
* Dockerfile의 커맨드 한줄 한줄이 레이어가 되고, 도커 내부적으로 해당 커맨드의 수행 결과가 캐싱된 레이어와 변화가 없음을 인지하고 캐싱을 시도한다.
    * 레이어의 변화를 인지하지 못하면 => 캐싱된 레이어를 사용
    * 레이어의 변화를 인지하면 => 새 레이어를 생성
* Dockerfile의 모든 명령어가 전부 레이어로 저장되어 캐싱되지는 않음
    * `WORKDIR` => Layer 저장 O. 캐싱 O
    * `RUN`, `ADD`, `COPY` => Layer 저장 O. 캐싱 O
    * `EXPOSE`, `LABEL`, `CMD` => Layer 저장X. 캐싱 X

조금 더 이해하기 쉬운 그림
<img width="842" alt="스크린샷 2023-02-27 오후 10 03 52" src="https://user-images.githubusercontent.com/57285121/221570973-d63a31b7-00b3-4078-abcf-96c0ce015fdc.png"> 

* 결론 : **Dockerfile의 명령어들이 Layer를 구성(Read-Only)하며 이것들이 모여 컨테이너가 실행하는(Runtime) 이미지가 된다.(Read-Write)**

### Dockerfile 최적화를 통해 이미지 빌드 속도 단축
* 이미지 레이어에 대한 이해를 위하여 -
* 아래에 두 개의 Dockerfile이 있다.
    * 설치해야할 의존성 패키지는 변화가 없고 단순 코드의 변경만 있다고 가정한다.

```bash
FROM node

WORKDIR /app

COPY . /app

RUN npm install

EXPOSE 80

CMD ["node", "server.js"]
```

```bash
FROM node

WORKDIR /app

COPY package.json /app

RUN npm install

COPY . /app

EXPOSE 80

CMD ["node", "server.js"]
```
* 첫 번째 Dockerfile은 로컬의 모든 파일을 컨테이너의 `/app` 경로에 COPY 하고 `npm install` 을 실행한다.
* 두 번째 Dockerfile은 `npm install` 을 실행하기 전에 `package.json` 파일을 `/app` 경로에 COPY 한다.

`npm install` 은 `package.json` 에 명시된 의존성 패키지를 설치하게 된다. 그러나 위 상황에서는 이전 레이어의 이미지와 비교했을 때 추가로 설치해야할 의존성 패키지가 없고 코드만 변경됐기 때문에 `npm install` 을 추가로 할 필요가 없다. 그렇기에 `package.json` 을 `/app` 경로에 COPY 이후 `npm install` 을 하게되면 새로 `npm install` 하는 것이 아닌 기존 레이어를 가져와 사용할 수 있게 되기에 이미지 빌드 속도가 단축될 수 있다.

* 또한 `Dockerfile` 의 모든 명령어가 전부 레이어로 구성되는 것은 아님.

## TAG 기반으로 이미지 관리하기
이미지를 빌드하고 나면, 임의의 이미지 ID가 부여되는데 이 ID로 이미지를 구별하는 것은 쉽지 않기에 이름과 태그를 통해 이미지의 
식별자를 만들어 관리한다. 이미지에 붙일 수 있는 식별자의 구조는 아래와 같다.
```
name : tag
```
* 특정 app의 이름을 name으로 지정하고, 해당 app의 버전을 태그로 사용하면 좋지 않을까 싶다.
    * app 이름이 trade라고 한다면, `trade:v1.1.0` 뭐 이런식으로 ..?
* 위 구조로 이미지를 빌드하고자 하면 빌드 하는 시점에 `-t` 옵션을 주고 이름과 태그를 지정해주면 된다.
    * 별도 태그를 지정하지않고 이름만 입력하면 latest로 빌드된다.
```bash
docker build -t {name:tag} . 
```

## 이미지 공유하기
빌드 결과로 생성된 이미지를 dockerhub에 push해보자. 사전에 dockerhub 계정이 준비되어 있어야 한다. free tier는 1개의 이미지만 올릴 수 있음.
1. dockerhub에서 repository 생성
2. local에서 `docker login`
    * login하지 않으면 Access denied 발생.. 웹에서 가입한 ID/Password로 로그인하자.
3. push
    * 이 때 dockerhub에서 생성한 repository의 이름과 push하고자 하는 이미지의 이름이 같아야한다. 만약 이미지의 이름이 생성한 repository의 이름과 다르다면 `docker tag` 커맨드로 수정하자.
        * `docker tag {local image} {remote image}` 
    * 그 후 `docker push {image}`

* public repository의 이미지 pull은 login 필요 없음. 
    * `docker pull {image}`

### 이미지 관련 command
```bash
# 이미지 목록 확인
docker images

# 이미지 제거
docker rmi {image} # 컨테이너가 사용중이지 않은 이미지일 경우에만 삭제 가능. 중지 상태의 컨테이너여도 삭제 불가. 오직 컨테이너가 삭제되었을 때만.

# 이미지 비우기
docker image prune # 어떠한 컨테이너에서도 사용중이지 않은 이미지 전부 삭제(태그 없는 이미지만 비움)
docker image prune -a # 이미지의 이름과 태그가 지정된 것도 전부 삭제

# 이미지 분석
docker image inspect {image}
```

