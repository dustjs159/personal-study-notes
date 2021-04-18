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
   
작업 내역을 바로 commit을 하지 않고, Staging Area를 경유하는 이유는 작업 내용을 한번 더 확인하여 선별적으로 Local Repository에 반영하기 위함   
   
Staging Area를 사용하게 되면 그렇지 않을 때보다 시간이 더 소요되지만 보다 더 안정된 버전관리 작업이 가능   

* Local Repository : git 프로젝트의 다양한 메타데이터와 데이터 정보가 들어있는 디렉토리   
    
git이 작업중인 파일에 대한 버전을 관리하기 위해서는 작업하고 있는 Working Directory를 git이 알아야 함   
   
Working Directory에 ```git init``` 이라는 명령어를 입력하면 해당 Working Directory는 git repository가 되고, 이 git repository를 Local Repository라고 함      
Local Repository 안의 .git폴더가 해당 디렉토리 안에서 일어나는 일들(변경, 수정사항 등)은 git이 실시간으로 알게 됨   
   
* Remote Repository : 원격지의 저장소

# add
* 스테이지에 올리기
* 커밋을 하기 전에 저장하고자 하는 파일들을 묶는 작업(= Stage에 파일을 올리는 작업) 
* ``` git add <file name> ```

# commit
* 게임의 세이브에 해당하는 작업을 git에서는 커밋이라고 한다(언제든지 커밋한 시점으로 돌아갈 수 있다)   
* 커밋을 할 때 저장하고자 하는 파일들을 묶어서 커밋을 수행
* 커밋을 하면 현재 작업중인 내용의 세이브 데이터가 내 컴퓨터에 저장이 됨

# push
* github에 업로드
* github에 업로드를 하게되면 다른사람과 공유할 수도 있고, 내 컴퓨터의 데이터가 날아가도 안전하게 다시 복구할 수 있음

# init
 

# Git 설치 (Linux - CentOS)   

![gitinstall](https://user-images.githubusercontent.com/57285121/115059382-745e3400-9f21-11eb-8400-12084c48d8ea.png)   

* Git을 사용할 Local Repository 디렉토리를 미리 만들것을 추천


# GitHub에 접속해서 Repository를 생성   

GitHub 링크 : [GitHub](https://github.com "github link")   

1. 계정 생성이 안되어있다면 계정 생성 후   
   
<img width="500" alt="gitinstall2" src="https://user-images.githubusercontent.com/57285121/115059665-d0c15380-9f21-11eb-969c-dbb1e59f5733.png">

2. Create repository   
   
<img width="500" alt="gitinstall3" src="https://user-images.githubusercontent.com/57285121/115059709-df0f6f80-9f21-11eb-874c-18d9768a1408.png">
   
3. Repoistory name 작성하고 Create repository
   
<img width="500" alt="gitinstall4" src="https://user-images.githubusercontent.com/57285121/115059748-edf62200-9f21-11eb-9c4c-4238b97e6ebf.png">
   
4. repository 생성(원격지의 저장소 생성 완료)   


# 파일 업로드

* add →  commit →  push

clone 후 add,commit,push

1. init : 초기화. 해당 디렉토리를 로컬 깃 저장소로 만들어 줌. 이 곳에서 작업 진행   
```git init```

2. add : 작업이 완료된 파일을 Staging Area에 올림. 아직 수정이 완료되지 않았거나 보완이 필요한 파일은 나중에 add 한다.    
```git add <파일명>```   

3. commit : Staging Area에 올라가 있는
### clone : 기존 원격 저장소의 디렉토리를 로컬 저장소로 복사해옴   
```git clone <원격 저장소 주소>```   

### status : 저장소의 깃 상태 확인 및 상태 변경이 필요한 파일 확인 가능   
```git status```

### add : 작업이 완료된 파일을 Staging Area에 올림. 아직 수정이 덜 되었거나 보완이 필요한 파일은 나중에 add.
```git add <파일명>```   

### commit : 어떤 순간 작업 공간의 상태를 저장한 것. 어떤 시점의 스냅샷. Staging Area에 올라가있는(정상적으로 add된) 파일들을 Local Repository에 올림.   
```git commit -m "commit메시지"```   

### push : Local Repository에 올라가 있던 파일을 Remote Repository에 올림   
```git push <원격 저장소 이름> <push 할 브랜치 이름>```   

### fetch : Remote Repository의 파일을 다운. 최신 이력 확인 가능   
```git fetch```   

### merge : 다른 브랜치에서의 작업을 합칠 수 있음   
```git merge <브랜치 이름>```   

### pull : Remote Repository의 파일을 다운+병합. 원격 저장소와 로컬 저장소의 동기화 역할도 함   
```git pull <원격 저장소 이름> <pull할 브랜치 이름>```   

### remote : 원격 저장소와 연결   
```git remote add <원격 저장소 이름><원격지 주소>```   

### branch : 작업을 분기해서 할 수 있는 것.
```git branch <브랜치이름>```

