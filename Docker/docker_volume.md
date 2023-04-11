💻 [Docker] Volume
==================
## Volume
* Docker에서의 볼륨

컨테이너가 실행되며 발생한 데이터(로그나 외부의 입력값 등)는 어디에 저장할 것인가? 만약 컨테이너 내부에만 저장한다면 컨테이너가 종료되면 데이터도 사라지게 될 것이다. 만약 사용자의 로그인 정보를 컨테이너 내부에만 저장하고 컨테이너를 종료하게 된다면 사용자는 다시 회원가입을 해야할 것이다. 때문에 컨테이너 내부에서 실행되는 앱의 데이터는 영속성을 가져야하는 경우가 있기에 컨테이너의 종료나 중지에 상관없이 보존되어야 한다.

* **컨테이너는 자체 파일 시스템을 갖고 있다.**
    * Dockerfile로 빌드할 때 `COPY` 커맨드로 호스트의 파일 시스템을 스냅샷으로 만들어(디렉토리의 구조 정도..) 컨테이너에서 사용할 뿐, 컨테이너가 작동하며 발생한 데이터는 로컬의 스냅샷을 통해 만들어지는 컨테이너 내부의 파일시스템에 저장된다.
* 따라서 **컨테이너를 한번이라도 종료하게 된다면 컨테이너 내부에 저장되어 있던 데이터가 모두 삭제된다.**
    * 컨테이너의 내부 파일 시스템에 저장이 되는 것이기 때문에 그렇다.
* 데이터의 영속성을 위해 컨테이너 내부에서 저장되는 데이터를 외부의 어딘가에 저장해야할 필요가 있다.

## 컨테이너 내부에 데이터가 저장되는 위치 지정하기
* 컨테이너 내부에서 발생한 데이터는 어디에 저장되는지 알 수 없기에 이미지에 명시적으로 컨테이너 내부에 데이터를 저장할 경로를 지정한 후 외부의 어딘가와 매핑할 것이다.
    * 그러기 위해서는 이미지를 빌드할 때, 먼저 컨테이너 내부에서 발생하는 데이터를 어디에 저장할 지 지정해야한다.
* Dockerfile에 `VOLUME` 커맨드를 추가한다. 그리고 **컨테이너 내부에서 생성되는 데이터를 저장할 디렉토리 경로를 입력해준다.** 여기에 입력한 경로는 컨테이너 외부의 디렉토리에 연결된다.
    * Array 형식으로 작성.
    * 이미지의 크기가 늘어난다.
```vim
...
...
VOLUME [ "{container directory path}" ]
...
```

## Docker가 컨테이너 데이터를 저장하는 방법 - Volume
* 지금까지 말했던 "컨테이너 외부" 라는 곳이 Docker 엔진이 관리하는 **볼륨(Volume)** 이라는 것이다.
* Docker의 볼륨은 **컨테이너 내부와 호스트가 매핑되어 공유 가능한 디렉토리.**
    * 도커 엔진에 의해 관리되며 별도의 설정을 하지 않을 경우 도커가 임의의 경로로 설정한다.

<img width="863" alt="스크린샷 2023-02-27 오후 11 46 44" src="https://user-images.githubusercontent.com/57285121/221595036-b66841d7-c6ef-4529-b674-7c4d85b7bc13.png">

* **호스트의 디렉토리와 컨테이너 내부의 디렉토리와 매핑하여 컨테이너 종료 후에도 호스트에 데이터가 남아있다.** 또한 이후 새 컨테이너를 실행할 때 호스트에 남아있던 데이터가 필요할 경우 볼륨을 연결하여 사용할 수 있다.

Docker에서 볼륨은 두 가지 유형이 있다.

* 익명의(Ananymous) 볼륨 : `-v 옵션 없이` 컨테이너를 실행할 경우에 생성되며 컨테이너 내부에서 관리
    * 이때 익명의 볼륨은 컨테이너 종료시 삭제(휘발성)
* 명명된(Named) 볼륨 : `-v` 옵션으로 호스트의 특정 디렉토리를 지정하여 해당 위치에 데이터 저장 
    * 이때 컨테이너를 종료해도 데이터가 남아있음
    * `docker run` 커맨드에 `-v` 옵션을 주어 특정 이름을 부여할 수 있다.
    * `-v {volume name}:{container fs}`

## Docker가 컨테이너 데이터를 저장하는 또 다른 방법 - BindMount
* 호스트의 디렉토리 하나를 컨테이너에 마운트하는 ...
* Bind Mount는 호스트에 매핑될 컨테이너의 경로를 설정한다. 볼륨에 저장되는 데이터들은 영구적으로 보관할 수는 있지만 편집은 할 수 없다. Bind Mount는 보관중인 데이터를 편집할 수 있다.


### 볼륨 관련 Command
```bash
# 볼륨 리스트
docker volume ls

# 볼륨 삭제
docker volume rm {VOLUME}
docker volume prune

```