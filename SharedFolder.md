Shared Folder
=======================
Local(Windows)에서 폴더를 생성하고 해당 폴더를 VM과 공유하기
-----------------------------------------------

# Local(Windows)에 폴더 생성 및 권한 설정

* 폴더 속성 > 공유 탭 > 공유 > 공유할 사람 Everyone 선택 및 사용 권한 수준 읽기/쓰기로 변경   
![share2](https://user-images.githubusercontent.com/57285121/115682414-67fa3100-a390-11eb-9c3b-970a1ede83f8.png)

* 폴더 속성 > 공유 탭 > 고급 공유 > 선택한 폴더 공유 체크 > 권한 > Everyone의 사용 권한 모든 권한 허용 체크   
![share3](https://user-images.githubusercontent.com/57285121/115682828-cde6b880-a390-11eb-89f8-c5e8f741b0c7.png)   

# Local(Windows)의 폴더를 VM에 마운트

* 디렉토리에 마운트 하기   
```mount -t cifs //<Local IP>/<공유폴더> <리눅스디렉토리> -o username=<ID>,password=<passwd>```   
![share4](https://user-images.githubusercontent.com/57285121/115685563-4babc380-a393-11eb-9454-661248273df7.PNG)

* df로 마운트 여부 확인   
``df``   
![share5](https://user-images.githubusercontent.com/57285121/115685774-80b81600-a393-11eb-9b85-46ebbd3f3c86.png)   

# Test   
![share6](https://user-images.githubusercontent.com/57285121/115685896-9f1e1180-a393-11eb-9c0a-fbfef892f5d6.PNG)
   
![share7](https://user-images.githubusercontent.com/57285121/115686005-bbba4980-a393-11eb-9edf-fe29cee39371.PNG)


