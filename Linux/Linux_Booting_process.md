💻 Linux Booting Process
=======================

# 💡 리눅스 부팅 과정

* Linux 운영체제의 Booting Process
* 전원이 공급되는 순간부터 사용 가능한 상태에 도달하기 까지의 과정

## 📌 BIOS 실행

* BIOS : Basic Input/Output System
* 부팅 시 가장 먼저 실행되는 펌웨어로써 전원 공급시 주변 하드웨어 Check
  * 여기서 말하는 하드웨어 Check는 디스크(HDD or SSD)의 **무결성** 검사(부팅 할 디스크가 잘못된 부분이 있는지 Check)
* 하드웨어를 Check하면서 **MBR(Master Boot Record)** 내 부트로더(Boot Loader)를 실행
  * **부트로더(Boot Loader)** : 메모리에 실행할 운영체제의 정보를 적재해주는 프로그램
  
## 📌 MBR(Master Boot Record)

* 부팅을 진행하기 위한 정보가 포함되어 있는 디스크 파티션
* 부팅 디스크의 첫 번째 섹터(512 byte)에 위치
* 1차 부트로더
  * 2차 부트로더인 GRUB를 실행

  
## 📌 GRUB(GRand Unified Bootloader) 

* OS의 용량이 커짐에 따라 부트로더를 1차와 2차로 나누어 부팅 진행
* 리눅스 시스템 로그인 시 볼 수 있는 첫 번째 화면
* 설치된 OS 중에서 부팅할 이미지 파일(e.g. Ubuntu 20.04-LTS.iso)을 선택하여 부팅 진행
* ``/boot/grub/grub.conf`` or ``/etc/grub.conf`` 에 Config 파일 위치
* GRUB Config 확인(Ubuntu 20.04 기준)

## 📌 Kernel

* 커널(Kernel) : 운영체제에서 가장 핵심적인 부분
* 커널은 GRUB 단계에서 선택한 부팅 이미지 파일의 커널은 ``grub.conf`` 설정에 따라 최상위 경로 root에 파일 시스템을 마운트
* 루트 파일 시스템 마운트 후, ``/sbin/init`` 실행
  * ``init`` 프로그램은 가장 먼저 실행 되며 ``pid``가 항상 1번
  

## 📌 Init
* 최근에는 ``Systemd``로 대체

### ✔️ Runlevel 

* Runlevel 0
* Runlevel 1
* Runlevel 3
* Runlevel 5
* Emergency
