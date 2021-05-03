Link in Linux
===================

# Link
* 파일을 가리키는 또 다른 파일
* 리눅스에서 윈도우의 바로가기와 같은 개념
* 원본 파일의 내용이나 링크로 생성된 파일의 내용에 변경사항이 생길 경우 두 파일 다 변경사항 적용
* 하드링크(Hard Link)와 심볼릭링크(Symbolic Link) 두 종류가 있음

# Hard Link
* 원본 파일과 똑같지만 다른 이름의 파일을 생성 
* 파일을 안전하게 보관하고 싶을 때 사용
* ln <원본파일> <하드링크로 생성할 파일의 이름>   
<img width="470" alt="스크린샷 2021-05-03 오후 9 14 25" src="https://user-images.githubusercontent.com/57285121/116874611-8bf12880-ac54-11eb-8210-67d8cd381e80.png">   

# Symbolic Link(Soft Link)
* 원본 파일의 바로가기를 생성 
* 경로 단축을 위해 사용
* ln -s <원본파일> <심볼릭링크로 생성할 파일의 이름>   
<img width="596" alt="스크린샷 2021-05-03 오후 9 16 15" src="https://user-images.githubusercontent.com/57285121/116874767-ce1a6a00-ac54-11eb-8fc3-8ae73b6e3334.png">   


