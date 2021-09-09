LAN / MAN / WAN
====================================
## Summary
- Last Updated : 21.09.09 Thu   
- Updated by : 윤연선
-----------------------------------

# 네트워크 형태
   
<img width="702" alt="스크린샷 2021-06-28 오후 2 10 32" src="https://user-images.githubusercontent.com/57285121/123583490-9bd35600-d81a-11eb-8401-36d6caea2358.png">
   
* 네트워크의 규모에 따라 구분
* LAN
* MAN
* WAN

# LAN(Local Area Network)
* **근거리 통신망**
* 회사 건물 내부, 가정 등 비교적 작은 범위의 네트워크

## LAN의 위치
   
<img width="856" alt="스크린샷 2021-06-28 오후 3 01 58" src="https://user-images.githubusercontent.com/57285121/123587815-cb399100-d821-11eb-9ffb-90e60c6ef5ce.png">
   
* LAN은 이더넷으로 구성되는 것이 대부분

# Ethernet
   
![ethernet1](https://user-images.githubusercontent.com/57285121/115180161-e98f5c00-a10f-11eb-8638-e819d738e0b8.PNG)   
   
* 이더넷은 OSI 7 계층중 1 계층(물리)과 2 계층(데이터 링크)에 대한 규격
* 장치 고유의 번호(MAC 주소) 기반 이더넷 통신
* 규격과 방식은 IEEE 802.3 표준을 구현
* **CSMA/CD** 방식을 사용하여 통신

## CSMA/CD
* Carrier Sense Multiple Access/Collision Detection   
> * Carrier Sense : 회선의 상태를 확인하고   
> * Multiple Access : 동시에 접근이 가능하게   
> * Collision Detection : 충돌을 검사하여 제어하는 통신 방식   
* 하나의 네트워크에 여러 호스트들이 동시에 데이터 통신을 하게 되면 충돌이 일어날 수 있는데, 데이터 전송 효율이 떨어지는 것을 막기 위해 사용하는 방식
* **Ethernet 통신에서는 대부분 CSMA/CD 방식을 사용**하여 통신

### 주요 절차
   
<img width="350" alt="스크린샷 2021-09-09 오후 12 36 22" src="https://user-images.githubusercontent.com/57285121/132618261-97551e3f-78ac-45ce-b2a5-ebcd5ced88ea.png">
   
1. 채널(회선) 감시 : 송신 전 회선의 사용 여부를 감시
2. 채널 Idle / Busy : 회선이 Idle 일 경우 데이터 전송, Busy 일 경우 계속 감시
3. 데이터 전송 및 채널 감시 : 지속적으로 채널을 감시하고 전송 중 데이터 충돌 여부 확인
4. Jam 신호 전송 : 데이터 충돌 발생 시 Jam 신호를 통해 충돌 발생을 통보받고 전송 중단
5. Backoff : 일정 시간 후 재전송을 시도. 이 때 시간을 Backoff 시간이라고 하는데 충돌이 계속해서 발생하게 되면 이 Backoff 시간이 지속적으로 증가하게 됨   
 
# MAN(Metropolitan Area Network)
* LAN과 WAN의 **중간 규모의 도시형 네트워크**
* LAN을 지역범위로 확대(Ex, 지역 CCTV 네트워크)

# WAN(Wide Area Network)
* LAN과 LAN을 이어 주기 위한 네트워크(Ex, 기업의 본사와 지사 연결)
* LAN에 비해 보다 광범위하고 규모가 큰 네트워크
* ISP(KT, SKT등의 통신 사업자망)를 사용하여 구축된 네트워크
