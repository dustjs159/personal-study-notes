Virtual Machine
====================================
## Summary
- Last Updated : 21.07.14 Wed   
- Updated by : 윤연선
-----------------------------------

# 가상머신(VM, Virtual Machine)
* 가상 머신은 물리적으로 존재하는 하나의 컴퓨터에서 여러 가상의 컴퓨터를 생성합니다.
* 1대의 PC에서 여러 OS들을 사용할 수 있습니다.
* 기존에 설치되어있던(물리적인) 컴퓨터의 OS를 **Host OS**라고 부르고 가상머신의 OS를 **Guest OS**라고 부릅니다.

## 가상머신 작동 원리
* 컴퓨터를 작동하기 위해 필요한 자원들(CPU, 메모리, 스토리지, NIC 등)을 각각 소프트웨어적으로 구현하는 **가상화 기술**을 기반으로 작동

### 가상화(Virtualization)
   
<img width="610" alt="스크린샷 2021-07-15 오전 12 39 57" src="https://user-images.githubusercontent.com/57285121/125650791-707884ce-5ad9-4aa7-8367-fabfe9afd5b7.png">
   
* 실제 물리적 장치의 기능을 논리적으로 구현하는 기술입니다. 따라서 실제 하드웨어 장치와 가상화 기술로 만들어진 장치는 같은 기능을 할 수 있습니다.
* 가상화의 대상이 되는 자원은 CPU, 메모리, 스토리지, NIC, GPU 등이 있습니다.
* 이러한 자원들을 가상화하여 여러 자원들을 묶어 하나의 장치로 사용하거나 혹은 그 반대로 하나의 장치를 나눠 여러 장치로 사용할 수 있습니다.
* 이렇게 가상화 기술을 통해 저렴한 비용으로 하나의 PC에서 다수의 시스템 운영이 가능합니다. 
* 하지만 물리적인 장치를 가상의 자원으로 구현을 한 만큼, 실제 장치보다는 성능이 조금 떨어집니다.

### 하이퍼바이저(HyperVisor)
   
<img width="603" alt="스크린샷 2021-07-15 오전 12 47 59" src="https://user-images.githubusercontent.com/57285121/125652055-b98b1669-d7ea-4fdf-a2bb-c0304b125db7.png">
   
* 가상머신과 하드웨어 중간에 위치하여 가상화 기술의 구현을 가능하게 도와줌
* Host OS의 실제 물리적 자원을 가상화하여 Guest OS에게 제공
* 가상머신 모니터링 기능도 수행
* 하이퍼바이저는 두 가지 유형이 존재
   
<img width="348" alt="스크린샷 2021-07-15 오전 1 38 46" src="https://user-images.githubusercontent.com/57285121/125659671-7deafb0c-a67c-40ee-bc56-17c9b1d2aa5e.png">
   
> * Type 1 : Native 혹은 Bare Metal 하이퍼바이저   
> * 하드웨어와 직접 상호작용   
   
<img width="326" alt="스크린샷 2021-07-15 오전 1 47 04" src="https://user-images.githubusercontent.com/57285121/125660826-a3449646-5bc1-4f14-a57c-38883a106aba.png">
   
> * Type 2 : Hosted 하이퍼바이저   
> * Host OS 위에서 작동   
> * VMware, Parallels, Virtual Box 등의 가상머신이 여기에 속함   

