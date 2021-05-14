IPsec
=========================

# IPsec(IP Security)
* Layer 3 - Network Layer에서의 보안을 위한 프로토콜
* IPsec의 동작모드 : 전송모드 / 터널모드

## 전송모드   
<img width="493" alt="스크린샷 2021-05-06 오후 9 16 09" src="https://user-images.githubusercontent.com/57285121/117296673-4a5cb980-aeb0-11eb-8d33-b6b97b4831af.png">   
* IP 패킷의 페이로드를 보호하는 모드. 즉 IP보다 상위 계층의 프로토콜의 데이터들을 보호   
* 상위 계층의 프로토콜만 보호하기 때문에 목적지 IP 주소와 출발지 IP 주소는 그대로 노출이 됨(보안에 있어서 약점이 될 수도 있음)   

## 터널 모드   
<img width="594" alt="스크린샷 2021-05-07 오전 1 11 16" src="https://user-images.githubusercontent.com/57285121/117330904-21005580-aed1-11eb-939e-f86ad6ce5d00.png">   
* IP 패킷 전체를 보호하는 모드. IP 패킷 전체를 IPsec로 캡슐화하면 IP 헤더를 식별할 수 없기 때문에 주소 정보를 담은 새 IP 헤더를 추가   
* 원본 IP 헤더를 보호하지만 새로 추가된 IP 헤더의 정보는 노출됨(제한적인 기밀성)   
* 새 IP 헤더에는 터널링이 시작되는 게이트웨이의 IP 주소만이 들어있음   

# IPsec 세부 프로토콜
* AH / ESP

## AH(Authentication Header)
* 인증을 담당하는 프로토콜   
<img width="491" alt="스크린샷 2021-05-07 오전 1 34 19" src="https://user-images.githubusercontent.com/57285121/117333878-59edf980-aed4-11eb-84bb-01d3053a6562.png">   
 
* AH 헤더에는 변경될 수 있는 필드를 제외한 나머지 필드 전체에 해쉬 함수를 적용한 인증 데이터 + 대칭키 암호화 방식을 사용한 인증키가 포함되어 있음   
* 수신측은 송신측이 전송한 인증 데이터를 검증   
* 인증과 데이터의 무결성은 제공하지만 암호화를 지원하지 않으므로 기밀성 보장은 되지 않음   

## ESP(Encapsulating Security Payload)
* AH에서 제공하는 보안성 뿐만 아니라 암호화 제공을 통한 기밀성까지도 보장   
<img width="589" alt="스크린샷 2021-05-07 오전 2 05 28" src="https://user-images.githubusercontent.com/57285121/117337740-b3f0be00-aed8-11eb-8050-ec5b46df3d15.png">   


