Booting
====================================
## Summary
- Last Updated : 21.06.08 Tue   
- Updated by : 윤연선
-----------------------------------

# 부팅(Booting)
* 사용자가 컴퓨터를 켜고 운영체제를 메모리에 불러오는 과정
* 본격적으로 컴퓨터를 사용하기 전에 필요

## 부팅 과정
1. 컴퓨터 전원을 누르면 메인보드와 메인보드에 부착된 장치들에게 전력이 공급
   
<img width="611" alt="스크린샷 2021-06-08 오후 1 30 41" src="https://user-images.githubusercontent.com/57285121/121123180-ba6ab080-c85d-11eb-9cc6-f27eb794b289.png">
   
2. CPU가 ROM(Read-Only Memory)에 저장된 BIOS를 실행
   
<img width="629" alt="스크린샷 2021-06-08 오후 1 34 00" src="https://user-images.githubusercontent.com/57285121/121123443-3107ae00-c85e-11eb-9af5-799a094df7ad.png">
   
3. BIOS는 POST(Power On Self Test) 과정을 통해 주변 하드웨어 장치들을 검사
   
<img width="626" alt="스크린샷 2021-06-08 오후 1 39 58" src="https://user-images.githubusercontent.com/57285121/121123939-05d18e80-c85f-11eb-9c8f-3adc5c36b1dc.png">
   
4. BIOS가 보조기억장치의 MBR(Master Boot Record)에 저장된 정보를 읽고 부트로더(Boot Loader)를 주기억장치 RAM(Random Access Memory)에 올리는 **부트스트랩(BootStrap)**과정을 실행
   
<img width="630" alt="스크린샷 2021-06-09 오전 12 43 11" src="https://user-images.githubusercontent.com/57285121/121216238-ace41380-c8bb-11eb-92c3-c24857804f24.png">
   
5. 부트스트랩(BootStrap)과정으로 RAM에 부트로더(Boot Loader)가 올라가고, 디스크의 OS(Kernel)코드를 복사하여 RAM에 붙여넣어 OS실행. OS가 실행된 후에는 제어권이 OS에게로 넘어감
   
<img width="641" alt="스크린샷 2021-06-09 오전 12 48 40" src="https://user-images.githubusercontent.com/57285121/121217057-70fd7e00-c8bc-11eb-8ece-4ea40828b808.png">
   
6. OS 부팅 완료
   
<img width="632" alt="스크린샷 2021-06-09 오전 12 49 39" src="https://user-images.githubusercontent.com/57285121/121217204-938f9700-c8bc-11eb-8f3e-4198f7e8834e.png">
   
## 부트로더(Boot Loader)
* OS를 RAM에 올려주는 프로그램

## 부트스트랩(BootStrap)
* OS를 RAM에 올리는 부트로더(Boot Loader)의 작업을 도와주는 과정
