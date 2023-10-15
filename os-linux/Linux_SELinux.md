SELinux
====================================
## Summary
- Last Updated : 21.07.10 Sat   
- Updated by : 윤연선
-----------------------------------

# SELinux
* SELinux(Security Enhanced Linux)는 보안에 취약한 리눅스를 보호하기 위해 접근 권한을 설정할 수 있는 도구
* 외부의 공격자가 시스템 경로에 침입을 하더라도 관련 설정파일을 읽거나 프로그램을 실행하지 못함
* SELinux의 설정파일은 /etc/sysconfig/selinux에 있음
* SELinux의 보안기능은 클라이언트 측에서는 활성화 하는것이 좋지만, 서버 측에서는 서비스간 충돌이나 네트워크에 문제가 생길 수 있기 때문에 비활성화(disabled)로 하는 것이 서버의 장애를 미리 예방할 수 있다.
* 하지만 보안적으로는 취약점이 생긴다는 점..

# SELinux의 보안 단계
   
<img width="749" alt="스크린샷 2021-07-10 오전 3 31 57" src="https://user-images.githubusercontent.com/57285121/125122168-f8464780-e12f-11eb-895b-6a1132c74de6.png">
   
* SELinux의 보안 단계는 3가지가 존재
* enforcing   
> * 활성화
* permissive   
> * 허용을 하지만 제한된 접근권한에 대하여 로그를 출력함   
> * 로그의 경로는 /var/log/audit/audit.log   
* disabled   
> * 비활성화   

# 관련 명령어
* ``$ sestatus`` : SELinux 보안 단계 확인

 
