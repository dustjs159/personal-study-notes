BIOS
====================================
## Summary
- Last Updated : 21.06.08 Tue   
- Updated by : 윤연선
-----------------------------------

# BIOS(Basic Input/Output System)
* CPU, 메모리, I/O 장치 등 컴퓨터의 하드웨어적 자원을 관리하는 일종의 펌웨어
* 컴퓨터의 하드웨어(주변 장치)와 소프트웨어(OS) 사이에 위치
* 컴퓨터 전원을 켜면 가장 먼저 실행되는 프로그램
* 전원이 공급되면 하드웨어를 초기화하고 검사하며 부팅 시작
* **ROM(Read Only Memory)에 저장**되어있음
* **POST(Power-On Self-Test)**   
> * 주변 장치(하드웨어) 검사(문제가 없는지)   
> * 컴퓨터 켜면 화면에 글자들이 출력되는 것을 확인할 수 있는데 이것이 BIOS가 POST과정을 통해주변 장치들을 검사하고 로그를 보여주고 있는 것   
* POST 과정 후 부팅 매체가 될 수 있는 것들 중 부팅 매체 선정(USB, HDD, SSD 등)

## Legacy BIOS
* 구형 BIOS 
* 16 bit 시스템
* 2 TB 이상의 저장장치를 인식하지 못함
* 최대 1 MB의 메모리만 접근 가능
* 부팅 시 저장장치의 MBR 부트섹터를 거친 후 OS를 실행(부팅 속도가 느림)
 

## UEFI(Unified Extensible Firmware Interface)
* 신형 BIOS
* 64 bit 시스템
* 2 TB 이상의 저장장치 인식 가능
* MBR 부트섹터를 거치지 않고 Boot Manager를 통해 바로 부팅(부팅 속도가 빠름)
* 사용자 친화적인 UI 덕분에 조작하기 쉬움
* POST과정이 눈에 보이지 않는 경우가 있음

# MBR(Master Boot Record)
* 저장매체의 첫 번째 Sector(512Byte)에 위치하는 영역
* 16Byte의 Primary Partition(주 파티션) 4개(64Byte) 혹은 주 파티션 3개와 확장 파티션 1개 + **부트로더(Boot Loader)**
* MBR로 설정할 수 있는 파티션 용량의 한계는 최대 2TB
* 32bit / 64bit OS 둘 다 지원
* Legacy / UEFI BIOS 둘 다 지원

# GPT(GUID Partition Table)
* 2TB이상의 파티션 사용 가능(최대 8ZB)
* 최대 생성 가능한 파티션 수가 128개
* 32bit OS, Legacy BIOS 미지원





