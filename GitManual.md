리눅스에서 Git을 사용 해보자
====================================
# Git 이란?
> 리누스 토르발즈가 개발한 분산형 버전 관리 시스템.   
> 많은 종류의 버전 관리 시스템이 있지만 그 중에서 압도적인 점유율을 차지하고 있다.

# Git의 주요 목적
1. Version 관리
2. Backup
3. Collaborate

# Git 동작 원리
> Git 프로젝트에 포함되어 있는 데이터들은 파일 시스템상에서 스냅샷 기능을 함(특정 시간에 파일을 복사 후 보관하여 백업 및 복구를 해줌)   
> 프로젝트를 commit하여 적용할 때의 순간을 포착   
> 파일 자체를 저장하기 보다 수정 내역 자체를 저장함   
![Alt text](https://github.com/dustjs159/gitstudy/blob/master/gitimage.png)
1. Working Directory : 작업중인 파일이 위치하고 있는 디렉토리
2. Staging Area : commit을 수행할 파일들이 올라가는 영역
3. Local Directory : Git 프로젝트의 다양한 메타데이터와 데이터 정보가 들어있는 디렉토리
4. Remote Repository : 원격지의 저장소

# Git 명령어 및 관련 용어
### init : 초기화. 해당 디렉토리를 로컬 깃 저장소로 만들어 줌   
```git init```

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

### clone : 기존 원격 저장소의 디렉토리를 로컬 저장소로 복사해옴   
```git clone <원격 저장소 주소>```   

### remote : 원격 저장소와 연결   
```git remote add <원격 저장소 이름><원격지 주소>```   

### branch : 또 다른 작업을 하고있는 다른 사용자의 이름. 브랜치 이름은 master가 아닌 다른 이름으로 하여 작업 완료 후 master브랜치와 병합
브랜치 생성 : ```git branch <브랜치이름>```

