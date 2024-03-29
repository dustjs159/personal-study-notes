💻 [Network] SSL/TLS
=====================
# SSL/TLS 
* SSL(Secure Socket Layer) / TLS(Transport Layer Security) : 데이터 "전송"시 보다 안전하게 데이터 전송을 하기 위한 암호화 프로토콜

## SSL(Secure Socket Layer)
* 서버와 클라이언트간 안전한 데이터 전송을 위한 암호화 프로토콜
* SSL 인증서를 통해 안전한 데이터 통신이 가능
* 데이터를 암호화해서 전송하기 위해 대칭키 암호화 방식과 공개키 암호화 방식을 혼합해서 사용

## HTTPS 에서 SSL을 이용한 안전한 통신 과정
* Handshake : 실제 데이터를 주고 받기 전 클라이언트와 서버가 탐색하는 과정   

1. 클라이언트가 서버에 접속(Client Hello). 이 때 클라이언트가 지원하는 암호화 방식 전송 + 클라이언트 측에서 생성한 랜덤 데이터 전송   
2. 서버가 클라이언트 요청에 응답(Server Hello). 이 때 서버가 지원하는 암호화 방식 전송 + 서버측에서 생성한 랜덤 데이터 전송 + **서버의 공개키가 포함된 SSL 인증서 전송**   
3. 클라이언트는 서버가 보낸 인증서가 CA(Certificate Authority, 인증기관)에서 발급된 것인지 확인하기 위해 CA 공개키로 인증서를 복호화하여 CA에서 발급되었다는 것을 증명 및 서버 신뢰    + 클라이언트측에서 생성한 랜덤 데이터와 서버측에서 생성한 랜덤데이터를 조합해서 Pre-Master Key(나중에 Session Key가 됨)를 생성하여 서버의 공개키로 암호화 후 전송    
4. 서버는 일련의 과정을 거쳐 Pre-Master Key를 Session Key로 변환, 획득 함   
5. HandShake 종료   

* Session Key로 대칭키 암호화 방식을 이용한 데이터 송, 수신   

**공개키 암호화 방식이 안전하게 데이터를 전송할 수 있다는 장점이 있지만 부하가 많이 소모된다는 단점이 있기 때문에 실제 데이터는 대칭키 암호화 방식으로 데이터를 주고 받되 대칭키에 사용되는 키는 공개키 암호화 방식으로 만들어서 데이터 노출을 최대한 피한다.**   

* 연결 종료 :  데이터 송, 수신 종료 시 서로에게 SSL종료를 알리고 통신에 사용된 Session Key폐기
   
<img width="712" alt="스크린샷 2021-05-15 오전 3 42 21" src="https://user-images.githubusercontent.com/57285121/118314774-90a8bd00-b52f-11eb-937a-dc909ccb4085.png">
   
# SSL 인증서   
* **1. 클라이언트가 접속한 서버가 신뢰 할 수 있는 서버임을 보장**   
* **2. 안전한 데이터 전송을 위한 데이터 암호화, 복호화 목적의 공개키를 클라이언트에게 제공**   

# SSL Offloading
* SSL 인증서 발급을 위해 클라이언트와 서버간 부하 발생
* 서비스를 제공해야하는 서버가 서비스 제공보다 인증에 더 많은 부하를 안게 됨
* 이러한 문제점을 해결하기 위해 Reverse Proxy를 사용하여 SSL인증서 암호화, 복호화를 담당하게 함
   
<img width="833" alt="스크린샷 2021-05-06 오후 4 23 23" src="https://user-images.githubusercontent.com/57285121/117257959-6ac44e00-ae87-11eb-8b51-73147b83a434.png">   
   
* 클라이언트와 Reverse Proxy는 HTTPS 통신을 하고 Reverse Proxy와 서버 그룹들은 HTTP 통신을 함   
* **Reverse Proxy 서버에 SSL 관련 작업을 위임**
* SSL Termination   
> * 일반적인 SSL 오프로딩의 구현 방법. 클라이언트와 Reverse Proxy는 SSL 연결을 통해 생성된 세션 키를 대칭키 방식으로 암호화를 하여 데이터를 주고 받으며 Reverse Proxy와 서버들의 그룹간에는 복호화된 데이터를 주고 받음   
> * Reverse Proxy의 부하를 줄여줌으로 성능 향상   
> * Reverse Proxy와 서버 그룹들간에는 보안성이 떨어질 수 있다는 단점 존재   
* SSL Bridging   
> * Reverse Proxy가 서버 그룹에게 데이터를 전송할 때 한번 더 암호화 과정을 거쳐서 데이터를 전송하는 방법   
> * SSL Termination의 보안 취약점을 개선할 수 있으나 Reverse Proxy는 암호화 과정을 한번 더 거쳐야 하므로 부하 상승으로 인해 성능이 떨어질 수도 있음   

# SSL 버전
1. SSL 1.0   
> * 일반인들에게 공개되지 않았던 버전.   
2. SSL 2.0
> * 넷스케이프사가 1995년에 발표한 버전.   
> Handshake과정에서 방어책이 없어 피해 가능성이 있었음(보안 취약점)    
3. SSL 3.0   
> * 1996년에 SSL 2.0의 심각한 결함을 해결하고 출시 된 버전.   
> * 보안취약점 존재 : POODLE(Padding Oracle On Downgraded Legacy Encryption)   

# TLS(Transport Layer Security)
* TLS는 역시 SSL과 마찬가지로 웹 서버와 클라이언트 간 통신을 암호화 하는데 사용되는 프로토콜.   
* TLS는 SSL 3.0을 기반으로 해서 국제 인터넷 표준화 기구인 IETF가 만든 프로토콜   
* SSL 3.0에서 보안성 및 안정성이 향상이 됨   
1. TLS 1.0   
> * SSL 3.0의 보안 취약점을 대부분 개선   
> * SSL 3.0으로 다운그레이드가 가능하다는 보안취약점 존재   
2. TLS 1.1   
> * 암호 블록 체인 공격에 대한 방어 추가   
> * IANA 등록 파라미터 지원 추가   
3. TLS 1.2   
> * 취약한 SHA1 해싱 알고리즘을 사용하지 않고 SHA2를 사용     
4. TLS 1.3   
> * 서버에서 인증서를 암호화하여 전달하도록 개선   
> * 강화된 보안(안전하지 않은 암호화 방식 지원X)   
> * 최초 연결 시에 암호화 통신을 개시하는 절차를 간소화하여 성능 개선    

