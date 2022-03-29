Backup
====================================
## Summary
- Last Updated : 21.08.29 Sun   
- Updated by : YEONSUN YOON
-----------------------------------

# 백업(Backup)
* 백업이란 데이터의 임시 보관을 말합니다. 혹시 모를 데이터 손실에 대비하여 임시로 사본을 만들어 문제 발생 시 언제든 복구할 수 있도록 준비합니다.

# 백업의 종류
* 백업의 종류는 크게 3가지가 있습니다.

## 전체 백업(Full Backup)
   
<img width="441" alt="스크린샷 2021-08-29 오전 3 59 05" src="https://user-images.githubusercontent.com/57285121/131228137-22ba5e7c-53fb-4fb1-bc4b-d033c56724a8.png">
   
* 전체 백업은 데이터 변경 유무와 관계 없이 데이터의 전체 복사본을 만드는 방식입니다.
* 장점 : 복구가 간편하고 복구 시간이 적게 소요
* 단점 : 많은 용량이 필요

## 증분 백업(Incremental Backup)
   
<img width="433" alt="스크린샷 2021-08-29 오전 4 04 55" src="https://user-images.githubusercontent.com/57285121/131228242-08b0f48b-fe2a-46e2-bca5-612c011624bd.png">
   
* 증분 백업은 일정 시간마다 변경된 데이터만 백업하는 방식입니다.
* 장점 : 파일 양이 적어 백업 시 빠른 백업이 가능
* 단점 : 전체 백업보다 복구 시간이 오래 걸림

## 차등 백업(Differential Backup)
   
<img width="432" alt="스크린샷 2021-08-29 오전 3 59 30" src="https://user-images.githubusercontent.com/57285121/131228146-45482264-ebb6-4b24-b623-aa32fb0d2bd3.png">
   
* 차등 백업은 최초에 전체 백업(Full Backup)후 변경된 모든 데이터를 백업하는 방식입니다.
* 장점 : 증분 백업보다 복구 시간이 적게 소요
* 단점 : 파일이 변경될 때마다 파일 크기가 증가


