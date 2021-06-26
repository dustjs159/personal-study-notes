Linux Boot 
====================================
## Summary
- Last Updated : 21.06.24 Thu   
- Updated by : 윤연선
-----------------------------------


# init & target 
* CentOS 7 이전의 시스템에 관련하여 init프로세스에서는 runlevel을 사용했었고 이후부터는 기존의 runlevel을 systemd target으로 대체
* /lib/systemd/system에 시스템에 관련된 target 파일들이 위치

## target unit
   
|init|target|설명|
|----|----|------|
|runlevel 0|poweroff.target|시스템 종료|
|runlevel 1|rescue.target|single-user 모드|
|runlevel 2|multi-user.target|multi-user 모드(미사용)|
|runlevel 3|multi-user.target|multi-user 모드|
|runlevel 4|multi-user.target|multi-user 모드(미사용)|
|runlevel 5|graphical.target|multi-user + graphic mode(GUI)|
|runlevel 6|reboot.target|시스템 재부팅|
 
