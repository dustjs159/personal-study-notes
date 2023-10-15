Git
====================================
## Summary
- Last Updated : 21.06.09 Wed   
- Updated by : 윤연선
-----------------------------------

# Git
* 리누스 토르발즈가 개발한 소프트웨어 버전 관리 도구
* 분산 저장소 방식 : 하나의 원격 저장소와 분산된 개발자의 로컬 저장소에 같이 저장되어 관리하는 방식
* 로컬 저장소에서 버전 관리가 가능하므로 원격 저장소에 문제가 생겨도 정상적으로 로컬 저장소에서 작업이 가능

# Git의 주요 목적
* Version 관리
* Backup
* Collaborate

# Git 동작 원리
* 2개의 저장소(Local Repository, Remote Repository)가 존재
* Local Repository : 실제 개발이 진행되는 장소. 버전 관리가 수행된다.
* Remote Repository : 여러 사람들이 협업을 위해 버전을 공동으로 관리. 자신의 버전 관리 내역을 반영하거나 다른 개발자의 변경내용을 가져올 때 사용.
* 파일의 변화를 스냅샷으로 저장, 스냅샷은 이전 스냅샷의 포인터를 가지므로 버전의 흐름 파악 가능
* 프로젝트를 commit하여 적용할 때의 순간을 포착   
* 파일 자체를 저장하기 보다 수정 내역 자체를 저장함   

# Git 작업 순서   

![gitimage](https://user-images.githubusercontent.com/57285121/115059311-57c1fc00-9f21-11eb-9bfc-de2c3d5f2034.png)   
* Working Directory : 작업중인 파일이 위치하고 있는 디렉토리   

* Staging Area : commit을 수행할 파일들이 올라가는 영역   
   
> * 작업 내역을 바로 commit을 하지 않고, Staging Area를 경유하는 이유는 작업 내용을 한번 더 확인하여 선별적으로 Local Repository에 반영하기 위함   
> * Staging Area를 사용하게 되면 그렇지 않을 때보다 시간이 더 소요되지만 보다 더 안정된 버전관리 작업이 가능   

* Local Repository : git 프로젝트의 다양한 메타데이터와 데이터 정보가 들어있는 디렉토리   
    
> * git이 작업중인 파일에 대한 버전을 관리하기 위해서는 작업하고 있는 Working Directory를 git이 알아야 함   
   
> * Working Directory에 ```git init``` 이라는 명령어를 입력하면 해당 Working Directory는 git repository가 되고, 이 git repository를 Local Repository라고 함      
> * Local Repository 안의 .git폴더가 해당 디렉토리 안에서 일어나는 일들(변경, 수정사항 등)은 git이 실시간으로 알게 됨   
   
* Remote Repository : 원격지의 저장소

# Git 주요 용어 
## add
* Staging Area에 올리기
* commit을 하기 전에 저장하고자 하는 파일들을 묶는 작업(= Stage에 파일을 올리는 작업) 
* ```git add <file name>```

## commit
* 게임의 세이브에 해당하는 작업을 git에서는 commit이라고 한다(언제든지 commit한 시점으로 돌아갈 수 있다)   
* commit을 할 때 저장하고자 하는 파일들을 묶어서 커밋을 수행
* commit을 하면 변경사항들이 git 디렉토리에 영구적인 스냅샷으로 저장
* ```git commit -m <commit message>```

## push
* github에 업로드(Local Repository의 변경 사항을 Remote Repository에 반영)
* github에 업로드를 하게되면 다른사람과 공유할 수도 있고, 내 컴퓨터의 데이터가 날아가도 안전하게 다시 복구할 수 있음
* ```git push <remote repo alias> <branch name>```

## init
* 해당 디렉토리를 git 디렉토리(Local Repository)로 만들어줌(깃 저장소 초기화)
* master branch를 자동으로 만들어 줌
* ```git init```

## remote
* Local Repository와 Remote Repository를 연결하거나 현재 연결되어있는 정보를 확인할 수 있음
* 연결 :  ```git remote add <remote repo alias> <remote repo URL>```
* 연결정보 확인 : ```git remote -v```

## clone
* Remote Repository의 파일들을 받아옴
* 자동으로 Remote Repository와 연결(git remote)
* 자동으로 Local Repository 초기화(git init)
* ```git clone <remote repo URL>```

## branch
* commit을 가리키고있는 일종의 포인터.
* 프로젝트의 master branch에서 다른이름으로 따와서 작업을 마친 후 master branch에 다시 merge함
* ```git init```을 통해 master branch가 자동으로 만들어짐
* HEAD : 현재 작업중인 branch를 가리킴
* ```git branch <branch name>```

## checkout
* 지정한 branch로 이동
* HEAD를 지정한 branch로 이동
* ```git checkout <branch name>```

## status
* git repository의 상태를 확인할 수 있음
* ```git status```

## merge
* master branch가 아닌 다른 branch에서 작업을 한 후에 다시 master branch로 병합을 할 때 사용
* 모든 변경사항을 master branch로 추가함
* ```git merge <branch name>```

## fetch
* Remote Repository의 최신 버전을 받아올 때 사용
* 병합은 진행하지 않고 저장소의 파일을 받아오기만 함
* 파일을 다운로드만 하고 병합을 하지 않기 때문에 병합 전, Local Repository와 Remote Repository의 차이점을 비교해 볼 수 있다.
* ```git fetch <remote repo alias> <branch name>```

## pull 
* Remote Repository의 최신 버전을 받아올 때  사용
* 병합도 추가적으로 같이 진행(다운로드 + 병합)
* ```git pull <remote repo alias> <branch name>```

## fork
* 타인의 github의 저장소에서 내가 어떤 부분을 수정하거나 추가 기능을 넣고 싶을 때 해당 저장소를 내 github저장소에 그대로 가져옴
* 타인의 저장소에 권한이 없는 사용자가 fork를 통해 가져온 내 저장소에 변경 사항을 push한 후 타인의 저장소에 Pull Request 요청을 보내고, 승인이 되면 타인의 저장소에 merge됨

# Git 사용하기

## GitHub에 접속해서 Repository를 생성   

* GitHub : [GitHub](https://github.com "github link")   

1. 계정 생성이 안되어있다면 계정 생성 후   
   
<img width="500" alt="gitinstall2" src="https://user-images.githubusercontent.com/57285121/115059665-d0c15380-9f21-11eb-969c-dbb1e59f5733.png">

2. Create repository   
   
<img width="500" alt="gitinstall3" src="https://user-images.githubusercontent.com/57285121/115059709-df0f6f80-9f21-11eb-874c-18d9768a1408.png">
   
3. Repoistory name 작성하고 Create repository
   
<img width="500" alt="gitinstall4" src="https://user-images.githubusercontent.com/57285121/115059748-edf62200-9f21-11eb-9c4c-4238b97e6ebf.png">
   
4. repository 생성(원격지의 저장소 생성 완료) 

## Git 설치 (Linux - CentOS)   

![gitinstall](https://user-images.githubusercontent.com/57285121/115059382-745e3400-9f21-11eb-8400-12084c48d8ea.png)   

* Git을 사용할 Local Repository 디렉토리를 미리 만들것을 추천

## Git Remote Repository에 파일 업로드(push)

1. git 디렉토리로 사용할 디렉토리 생성 : ```mkdir 디렉토리명```

2. git 디렉토리 초기화 : ```git init```

3. Remote Repository 추가 : ```git remote add <remote repo alias> <remote repo URL>```

4. add : ```git add <file name>```

5. commit : ```git commit -m "<commit message>"```

6. push : ```git push <remote repo alias> <branch name>```

## Local Repository로 파일 다운로드(pull)

1. git 디렉토리로 사용할 디렉토리 생성 : ```mkdir 디렉토리명```

2. git 디렉토리 초기화 : ```git init```

3. Remote Repository 추가 : ```git remote add <remote repo alias> <remote repo URL>```

4. pull : ```git pull <remote repo alias> <branch name>```

# Github 2 factor 인증

* 2중 인증
* ID/PW외에 추가적인 인증수단을 통해 계정을 보호

1. Github -> Settings -> Account security

2. Two-factor authentication 의 Enable two-factor authentication 클릭   
   
<img width="759" alt="스크린샷 2021-06-11 오전 3 11 00" src="https://user-images.githubusercontent.com/57285121/121579118-5f57da00-ca66-11eb-913e-b28755026c6b.png">
   
> * 이 때 생성되는 복구 코드는 따로 보관해 두도록 한다   

3. 모바일에 `Google Authenticator`어플 다운 후 QR코드 확인

4. 인증 번호 확인 후 2 factor 인증 활성화

## Command Line

* push가 안되길래..

1. Github -> Settings -> Developer settings -> Personal access tokens

2. Note에 이름 등록 후 접근 권한 설정

3. 생성한 토큰을 복사하고 push 할 때 사용자 계정 + 토큰을 입력해주면 push 성공
 
