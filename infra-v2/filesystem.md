File System
================
* Linux/Unix 계열 파일시스템만 작성.

### Definition
* 운영체제에서 저장장치에 데이터를 저장하고 관리하기 위한 구조 그 자체
* 종류 (자주 사용하는 두 종류만)
    * `ext4`
    * `xfs`

### `/etc/fstab` 
* OS 부팅 단계에서 마운트되어야 할 파일시스템 정보가 기록된 파일
* 각 필드의 의미
```
[device] [mountpoint] [filesystem type] [option] [dump] [filesystem check] 
```