Node.js Install & Set
=================================
## Summary
- Last Updated : 21.07.09 Fri    
- Updated by : 윤연선
---------------------------------
## Node.js 설치과정과 구성환경 및 실습 테스트
* 본 글은 CentOS 8 환경에서 작성했습니다. 
---------------------------------

# Node.js 설치

1. yum을 이용하여 Node.js 설치   
> * ``$ yum install nodejs``   
* 설치 과정 중, 의존성에 의해 npm과 'nodejs-full-i18n'이라는 모듈이 설치 되는 것을 확인
   
<img width="740" alt="스크린샷 2021-07-09 오후 9 58 49" src="https://user-images.githubusercontent.com/57285121/125081325-d84b5f80-e100-11eb-84fb-72c1340d0fc1.png">
   
2. 방화벽 허용 포트 설정
> * ``$ firewall-cmd --permanent --add-port=18080/tcp``   
> * ``$ firewall-cmd --reload``   

3. 웹 서버 파일 생성   
> * ``$ vi webtest.js``   

```javascript
var http = require('http');

port = '18080';
hostname = '172.16.123.14'; 

httpd = http.createServer(function (req, res) {
        res.writeHead(200, {'Content-Type':'text/html'});
        res.end('hello man');
});

httpd.listen(port, hostname, function(){
        console.log('server start');
});
```
4. 실행 테스트   
> * ``$ node webtest.js``
   
<img width="379" alt="스크린샷 2021-07-09 오후 10 38 18" src="https://user-images.githubusercontent.com/57285121/125086211-5e1dd980-e106-11eb-9029-cb903fefa75e.png">
   
<img width="356" alt="스크린샷 2021-07-09 오후 10 39 15" src="https://user-images.githubusercontent.com/57285121/125086340-7f7ec580-e106-11eb-8166-95d21cfa599a.png">
   
## PM2를 사용하여 백그라운드에서 실행
* ``$ node`` 명령어를 사용하여 웹 서버를 작동하게 되면 해당 작업 이외의 작업을 하지 못하게 됨
* PM2라는 nodejs 프로세스 매니저를 통해 웹 서버를 백그라운드에서 실행 가능하도록 함

1. npm을 통해 PM2 설치   
> * ``$ npm install pm2 -g`` (옵션 -g : global)   
   
<img width="757" alt="스크린샷 2021-07-09 오후 11 07 14" src="https://user-images.githubusercontent.com/57285121/125090536-6710aa00-e10a-11eb-84fc-194a0e45aba9.png">

2. 웹에서 접속 및 테스트   
> * ``pm2 start webtest.js``
   
<img width="718" alt="스크린샷 2021-07-09 오후 11 08 00" src="https://user-images.githubusercontent.com/57285121/125090630-827bb500-e10a-11eb-81d1-cf33dc2cbfcb.png">
   
<img width="355" alt="스크린샷 2021-07-09 오후 11 08 35" src="https://user-images.githubusercontent.com/57285121/125090688-99220c00-e10a-11eb-8090-51d449e51029.png">
   
### PM2 사용법
* PM2 상태 확인   
> * ``$ pm2 status``   

* PM2 시작   
> * ``$ pm2 start <파일명>.js``   
> * ``$ pm2 start <파일명>.js --watch`` : 소스파일 변경 사항을 자동으로 반영하여 자동으로 reload   

* PM2 중지   
> * ``$ pm2 stop <파일명>.js``   

* PM2 프로세스 종료   
> * ``$ pm2 kill``   

* PM2 로그 실시간 확인   
> * ``$ pm2 log``   
> * 추가적으로, PM2의 로그 목록은 ~/.pm2/logs에 기록됨
      
<img width="533" alt="스크린샷 2021-07-09 오후 11 33 27" src="https://user-images.githubusercontent.com/57285121/125094252-11d69780-e10e-11eb-94cc-b3a45fb5a1a3.png">
   
* PM2 모니터링   
> * ``$ pm2 monit``   

## 도메인으로 nodejs 웹 서버에 접속
* 웹 서버의 IP 주소가 아닌 도메인으로 웹 서버에 접속

   
 
