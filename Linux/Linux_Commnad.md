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
* Netcat : TCP/UDP를 통한 네트워크 연결
* 옵션
  * `-v` : ?
  * `-z` : ?
* 예시
```
$ nc -vz google.com 443

Connection to google.com port 443 [tcp/https] succeeded!
```
