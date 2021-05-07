Storage
===========================

# Storage
* 데이터를 저장할 수 있는 장소
* 직접 서버에 연결이 가능
* 대용량의 데이터를 저장하기 위해 별도의 네트워크 스토리지 구축 가능
* 호스트(클라이언트/서버)와 저장장치를 어떻게 연결하느냐에 따라 DAS, NAS, SAN으로 구분

# DAS
* Direct Attached Storage
* HDD를 여러 개 장착한 스토리지
* 유선으로 외장하드처럼 사용이 가능함   
<img width="480" alt="스크린샷 2021-05-06 오후 4 56 47" src="https://user-images.githubusercontent.com/57285121/117262297-0f488f00-ae8c-11eb-927f-3fadf1c54aae.png">   

* 호스트에 직접 꽂아서 1:1로 사용(USB처럼)
* 각 호스트는 자신이 직접 파일 시스템 관리
* 장점   
> * 저장장치를 직접 연결하므로 속도가 빠르며 확장이 쉽다  
> * 저장장치까지 가까운 곳에서 접근이 가능   
* 단점   
> * 연결 수에 한계가 있음   
> * 호스트 장애 시 스토리지 접근이 제한됨   
> * 물리적 공간이 부족할 때 확장이 어려움   

# NAS
* Network Attached Stroage
* DAS에 네트워크 기능을 탑재
* 호스트와 저장장치가 스위치를 통해 네트워크(LAN)에 연결됨
<img width="711" alt="스크린샷 2021-05-06 오후 5 03 31" src="https://user-images.githubusercontent.com/57285121/117263196-fee4e400-ae8c-11eb-9268-75e6b92a6b8d.png">   

* 주요 프로토콜   
> * FTP(File Transfer Protocol)   
> * NFS(Network File System)   
* 장점   
> * 네트워크를 통해 데이터를 저장 및 공유하므로 빠른 네트워크 속도를 통한 전송 속도 향상 가능   
* 단점
> * 네트워크의 접속자가 많아지면 성능이 저하될 수 있고 DAS에 비해 속도가 느림   

# SAN
* Storage Area Network
* 여러 스토리지를 하나의 네트워크에 연결하고 연결한 네트워크를 스토리지 전용 네트워크(SAN)로 구성
* 스토리지에 접근하려면 각 호스트들은 모두 SAN네트워크를 거쳐서 접근해야함 
* 별도의 SAN 스위치가 필요함
<img width="711" alt="스크린샷 2021-05-06 오후 5 08 17" src="https://user-images.githubusercontent.com/57285121/117263883-ab26ca80-ae8d-11eb-9703-52743f78de42.png">   

* FC-SAN(Fiber Channel SAN) : 광 케이블을 이용하여 스토리지에 접근
* IP-SAN : IP를 이용하여 스토리지에 접근
* 장점   
> * 확장성이 좋음   
* 단점 
> * 구성에 따라 네트워크 복잡도가 높아짐
