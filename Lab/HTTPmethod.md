HTTP Method Test
===================


* Rest API 검색 사이트 : https://reqres.in/
* 샘플 API가 있음   
![siteui](https://user-images.githubusercontent.com/57285121/116713682-fbc2a180-aa0f-11eb-837b-24431191638d.png)
* curl 명령어 이용
* 옵션   
> * -l : 헤더만 가져오기   
> * -i : 헤더와 바디 모두 가져오기   

# GET
* URL의 리소스를 요청하는 메소드
* curl -X GET <URL name>   
<img width="721" alt="스크린샷 2021-05-07 오후 5 22 17" src="https://user-images.githubusercontent.com/57285121/117421602-a4658980-af59-11eb-8cf9-9aaf62fcc814.png">   

* 요청에 대한 응답을 보여줌

# POST
* URL의 리소스에 데이터를 입력하는 메소드
* curl -X POST <URL name> -d <data>   
<img width="720" alt="스크린샷 2021-05-07 오후 5 24 19" src="https://user-images.githubusercontent.com/57285121/117421824-df67bd00-af59-11eb-898c-bf200fe3e1be.png">   
* 웹 페이지에 입력할 데이터를 같이 입력해 주면 입력 후 결과의 응답을 보여준다


# PUT
* 파일을 업로드하는 메소드 
* curl -X PUT <URL name> -T <업로드할 파일>   
<img width="720" alt="스크린샷 2021-05-07 오후 5 24 19" src="https://user-images.githubusercontent.com/57285121/117421824-df67bd00-af59-11eb-898c-bf200fe3e1be.png">

# DELETE
* 리소스를 삭제하는 메소드 
* curl -X DELETE <URL name> -d <삭제할 리소스>   
<img width="728" alt="스크린샷 2021-05-07 오후 5 25 46" src="https://user-images.githubusercontent.com/57285121/117422042-22c22b80-af5a-11eb-8658-fe368ae8ca9c.png">   

