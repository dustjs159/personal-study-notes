Link in Linux
===================

# Link
* 파일을 가리키는 또 다른 파일
* 리눅스에서 윈도우의 바로가기와 같은 개념
* 하드링크(Hard Link)와 심볼릭링크(Symbolic Link) 두 종류가 있음

# i-node
* 리눅스 파일시스템에서 사용하는 자료구조
* 파일이나 디렉토리의 소유권, 허가권, 파일 종류 등의 파일에 대한 정보(메타데이터)가 포함되어 있음   
<img width="835" alt="스크린샷 2021-05-03 오후 9 45 32" src="https://user-images.githubusercontent.com/57285121/116877422-e5f3ed00-ac58-11eb-83e3-5c2799f44fa1.png">   

# Hard Link
* 원본 파일과 똑같지만 다른 이름의 파일을 생성 
* 원본 파일의 inode를 가짐
* 파일을 안전하게 보관하고 싶을 때 사용
* ln <원본파일> <하드링크로 생성할 파일의 이름>   
<img width="470" alt="스크린샷 2021-05-03 오후 9 14 25" src="https://user-images.githubusercontent.com/57285121/116874611-8bf12880-ac54-11eb-8210-67d8cd381e80.png">   

* 원본 파일을 삭제해도 하드링크 파일은 삭제되지 않고 보존   
<img width="463" alt="스크린샷 2021-05-03 오후 10 53 17" src="https://user-images.githubusercontent.com/57285121/116885008-5ce1b380-ac62-11eb-8bec-460368aaa011.png">   

# Symbolic Link(Soft Link)
* 원본 파일의 바로가기를 생성
* 원본 파일의 주소를 가리키는 새로운 inode를 가짐 
* 경로 단축을 위해 사용
* ln -s <원본파일> <심볼릭링크로 생성할 파일의 이름>   
<img width="596" alt="스크린샷 2021-05-03 오후 9 16 15" src="https://user-images.githubusercontent.com/57285121/116874767-ce1a6a00-ac54-11eb-8fc3-8ae73b6e3334.png">   

* 원본 삭제시 심볼릭링크 파일도 삭제   
<img width="596" alt="스크린샷 2021-05-03 오후 10 49 59" src="https://user-images.githubusercontent.com/57285121/116884621-e644b600-ac61-11eb-9c30-bbe2afa7bd22.png">   

# Hard Link & Symbolic Link   

<img width="896" alt="스크린샷 2021-05-03 오후 9 44 39" src="https://user-images.githubusercontent.com/57285121/116877339-c6f55b00-ac58-11eb-8a7c-8141724b461c.png">

