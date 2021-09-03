Network Bonding
=================================
## Summary
- Last Updated : 21.07.01 Thu    
- Updated by : 윤연선
-----------------------------------

# Bondig 구성

1. Bonding 인터페이스 추가(ifname : mybond0)   
> * ``$ nmcli con add type add bond ifname mybond0``   
   
<img width="723" alt="스크린샷 2021-07-02 오후 5 19 26" src="https://user-images.githubusercontent.com/57285121/124244205-a7e05000-db59-11eb-8de4-0e709abe9769.png">
   
2. Bonding 인터페이스의 옵션 추가   
> * ``$nmcli con add type bond ifname mybond0 bond.options "mode=active-backup, miimon=1000"``   
* 옵션   
> * mode=active-backup : 인터페이스 장애 발생 시 다른 인터페이스 활성화(이중화)   
> * miimon : 모니터링 수행 단위 시간(ms 단위)   
   
<img width="756" alt="스크린샷 2021-07-02 오후 3 27 28" src="https://user-images.githubusercontent.com/57285121/124230475-043b7380-db4a-11eb-8b38-3106240ebc39.png">
   
3. Bonding할 인터페이스 생성 및 지정 (둘 이상)
* master(mybond0) - (slave(ens33) + slave(ens37))   
> * ``$ nmcli con add type ethernet ifname ens33 master mybond0``   
> * ``$ nmcli con add type ethernet ifname ens37 master mybond0``   
  
<img width="723" alt="스크린샷 2021-07-02 오후 5 21 59" src="https://user-images.githubusercontent.com/57285121/124244544-03aad900-db5a-11eb-90fd-f66d28eb9f9a.png"> 
   
* 'bond-slave-ens33', 'bond-slave-ens37' 생성

4. slave 활성화
> * ``$ nmcli con up bond-slave-ens33``   
> * ``$ nmcli con up bond-slave-ens37``   
   
<img width="725" alt="스크린샷 2021-07-02 오후 5 23 46" src="https://user-images.githubusercontent.com/57285121/124244766-4371c080-db5a-11eb-8c1c-6a723dfa1903.png"> 
  
5. bond 네트워크 활성화   
> * ``$ nmcli con up bond-mybond0``   
   
<img width="726" alt="스크린샷 2021-07-02 오후 5 32 00" src="https://user-images.githubusercontent.com/57285121/124245924-6b155880-db5b-11eb-9530-cc24f80374a4.png">
   
6. 장치 상태 및 네트워크 테스트   
* /proc/net/bonding의 bond 설정파일 확인
   
<img width="509" alt="스크린샷 2021-07-02 오후 5 33 58" src="https://user-images.githubusercontent.com/57285121/124246223-b0d22100-db5b-11eb-9fb2-b569f07dc411.png">
   
* ifconfig 확인
   
<img width="684" alt="스크린샷 2021-07-02 오후 5 35 16" src="https://user-images.githubusercontent.com/57285121/124246421-deb76580-db5b-11eb-8a6c-f8a0bdfa9643.png">
   
* ping 확인
   
<img width="541" alt="스크린샷 2021-07-02 오후 5 36 10" src="https://user-images.githubusercontent.com/57285121/124246555-fe4e8e00-db5b-11eb-911e-ef4cceb13f73.png">
   

