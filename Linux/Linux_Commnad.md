💻 Linux Command
===============
# 💡 Linux Commnad 

* Linux/Unix Command 모음
* 자주 사용하는 Command + 자주 사용하지 않더라도 알고 있으면 유용한 Command
* 테스트 환경은 MacOS 터미널 or Ubuntu에서 진행


### cut
* 파일이나 문자열을 Slice
* 옵션
  * `-c, --characters` : 문자열 기준으로 cut
  * `-d, --delimiter` : 구분자 지정. 지정한 구분자를 기준으로 왼쪽부터 필드값이 1번이 됨
  * `-f, --fileds` : 필드값을 기준으로 cut
* 예시

`text.txt`
```
EC2-AutoScaling
VPC-NATGateway
RDS-Aurora
```
`$ cut -c 2-7 text.txt`
```
C2-AutoS
PC-NATGa
DS-Auror
```
`$ cut -d '-' -f 2 test.txt`
```
AutoScaling
NATGateway
Aurora
```

### nc
* Netcat : TCP/UDP의 Connection 및 Listen Check
  * 클라이언트와 서버 간 통신이 안될 때 점검 용도로 많이 사용
* `$ nc [options] host port`
* 옵션
  * `-v` : 더 많은 정보를 확인할 수 있음(?)
  * `-z` : 최소한의 데이터만 전송(?)
* 예시
```
$ nc -vz google.com 443

Connection to google.com port 443 [tcp/https] succeeded!
```

### nohup

*  세션 종료 시에도 프로세스 무중단
* `wget` 이나 `curl` 명령어를 사용하여 용량이 큰 파일을 다운로드 받을 때, 터미널 로그인 세션 시간이 종료되면 Parents Shell에게 **SIGHUP(HUP)** Signal을 보내고 프로세스가 종료됨
* 이 때 `nohup` 명령어와 `&` 를 조합하여 세션 시간 종료 후에도 계속해서 다운로드를 진행(Background)
* 예시
```
$ nuhup 
```


### more

### grep

### du


### lsblk

### arp