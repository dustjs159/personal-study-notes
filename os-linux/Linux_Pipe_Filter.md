Pipe & Filter
====================================
## Summary
- Last Updated : 21.06.14 Mon   
- Updated by : 윤연선
-----------------------------------

# 파이프(Pipe)
* 두 개의 프로그램을 연결해주는 연결통로의 의미
* 이전 명령어의 결과를 다음 명령어의 입력값으로 사용 가능
* '|' 문자 사용

# 필터(Filter)
* 필요한 것만 걸러주는 명령어
* **grep**, tail, head, more 등
* 주로 파이프와 같이 사용

# 명령어
* ```cat <file> | grep 'abc'``` : file에서 abc를 포함한 문자열 출력
* ```cat <file> | tail``` : file의 내용중 마지막 라인 10줄만 출력
* ```cat <file> | head``` : file의 내용중 첫 라인 10줄만 출력 
* ```ls -l /etc | more``` : /etc의 파일 목록을 한 화면씩 나누어서 출력



