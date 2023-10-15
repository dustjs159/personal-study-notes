VM Network Setting
=====================================
   
![vmnet1](https://user-images.githubusercontent.com/57285121/115063468-9312f980-9f26-11eb-9d26-715d7490baac.png)   
   
* Bridged : 공유기로부터 IP를 할당 받아 호스트와 동일한 네트워크 대역의 IP를 갖게 됨. 공유기를 통해 외부 네트워크와 통신이 가능
* NAT : 호스트로부터 IP를 할당 받아 가상머신 프로그램이 자체 DHCP서버를 띄워 내부 네트워크 대역 할당 및 통신을 함. 호스트를 통해 외부 네트워크와 통신이 가능함.
* Host-only : 외부와 단절된 내부 네트워크를 구축. 구성된 가상머신들 끼리만 통신이 가능함
   
![vmnet2](https://user-images.githubusercontent.com/57285121/115063605-bccc2080-9f26-11eb-878d-563f6168c5f1.png)   
   

# Network Interface ON/OFF
VM설치 후에 네트워크와 관련된 별 다른 설정 없이 VM을 실행하면 인터넷 접속을 하지 못할 것이다

1. 컴퓨터 네트워크 상태를 점검하기 위해 ping명령어로 네트워크 상태 확인   

![vmnet3](https://user-images.githubusercontent.com/57285121/115063954-3ebc4980-9f27-11eb-80f6-38332b0c0166.png)   


2. /etc/sysconfig/network-scripts 디렉토리로 이동 후 자신의 네트워크 인터페이스 이름 확인   
   
![vmnet4](https://user-images.githubusercontent.com/57285121/115064130-880c9900-9f27-11eb-858e-359c141c0eb3.png)   
   
ifconfig 명령어로도 확인 가능(네트워크 인터페이스 정보 출력)   
   
![vmnet5](https://user-images.githubusercontent.com/57285121/115064308-bd18eb80-9f27-11eb-9daa-468fabc5a4bb.png)   
   

3. ifup 명령어로 네트워크 인터페이스 활성화

![vmnet6](https://user-images.githubusercontent.com/57285121/115064500-f0f41100-9f27-11eb-806f-b13273a37902.png)   
   
ifup <네트워크 인터페이스 명>   
비활성화를 할 때에는 ifdown을 사용하면 된다.

4. 활성화 후 ping 명령어로 네트워크 상태 확인
   
![vmnet7](https://user-images.githubusercontent.com/57285121/115064667-27319080-9f28-11eb-944e-a91bd961404e.png)   
   
잘 된다.
   
그런데 VM 재부팅을 하게되면 다시 비활성화 상태가 된다.   
그래서 부팅 시 자동으로 활성화를 해주기 위해서는 /etc/sysconfig/network-scripts의 ifcfg-ens33파일을 수정해야 함   
   
![vmnet8](https://user-images.githubusercontent.com/57285121/115064953-80012900-9f28-11eb-99ab-2d1de778f0c3.png)   
   
여기서 ONBOOT가 자동 실행 여부를 나타내는데, no에서 yes로 변경해 준다.




