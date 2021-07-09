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
   


