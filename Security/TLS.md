# [Security] TLS

`TLS(Transport Layer Security)` 및 그 이전 버전인 `SSL(Secure Socket Layer)` 은 인터넷에서 통신할 때의 인증 및 통화 암호화 장치이다.

# SSL(Secure Socket Layer)

`SSL` 은 웹 표준 암호화 통신으로 웹 서버와 브라우저 사이의 모든 정보를 암호화 해주는 방식이다. 이는 `http` 가 아닌 `https` 통신채널을 사용하며 모든 웹서버와 브라우저가 `SSL` 을 지원한다.

`SSL` 은 **서버인증, 클라이언트인증, 데이터 암호화 기능을 제공**한다

### HTTPS

- HTTP SECURE
- HTTP와 달리 HTTPS는 전송 데이터를 암호화함
- 통신 과정에서 데이터가 노출될 가능성이 적다
- 통신하고자하는 서버가 신뢰할 수 있는지 판별
- HTTPS는 암호화를 위해 `SSL/TLS` 프로토콜을 사용

# SSL 과 TLS

SSL은 네스케이프에 의해 발명되었고, SSL3.0이 표준화 된 이후 IETF의 관리로 변경되면서 TLS로 이름이 변경되었다. TLS 1.0은 SSL 3.0을 계승하였지만 TLS라는 이름보다 SSL이라는 이름이 더 많이 사용되고 있다

## 주요 기능

1. 신원 확인
    
    클라리언트가 접속한 서버가 신뢰할 수 있는 서버임을 보증
    
2. 메시지의 비밀 보장
통신에 사용할 공개키를 클라이언트에게 전달
    - 웹 서버와 고객간의 교환된 정보를 하나의 Session키로 암호화
    - 이 Session키를 전달하기 위해 공개키로 암호화하여 보냄
    - Session 키는 한번만 사용됨
    - 각 Session에 클라이언트 한명 당 하나의 키가 사용되어 제 3자가 볼 수 없게 함
3. 메시지의 무결성
    
    메세지 전송 시, 수신자와 발신자의 컴퓨터에서 암호 방식 생성
    

## 대칭키와 공개키

대칭키로 전송되는 데이터를 암호화하고, 대칭키를 공개키기법으로 암호화하여 전송하는 방법

SSL/TLS는 대칭키, 공개키를 함꼐 사용한다.

### 대칭키 방식

1. **암호화와 복호화를 동일한 하나의 키** (대칭키)로 하는 방식
2. 암호 통신을 하기 위해선 대칭키를 주고 받아야 하기 때문에 유출될 가능성이 있다 
→ 따라서, **공개키 기법으로 대칭키를 암호화하여 전송**한다

### 공개키  방식

1. **두개의 키 (공개키, 비밀키)로 암호화 및 복호화**하는 방식
2. 공개키로 암호화 → 비밀키로 복호화
3. 비밀키로 암호화 → 공개키로 암호화

공개키 방식은 보안이 뛰어나지만, 암호화/복호화에 컴퓨팅 파워가 많이 들어서 데이터 전달에는 대칭키를 쓰고 대칭키를 교환할 때 공개키를 사용

## 알고리즘

1. 상호인증
클라이언트와 서버간의 상호인증 (RSA, DSS, X.509), 공개키
2. 기밀성
대칭키 암호화 알고리즘을 통해 데이터 암호화 (DES, 3DES, RC4 등)
3. 데이터 무결성
MAC 기법을 이용해 데이터 변조 확인

## 동작 원리 - HandShake 과정

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e59362f5-1f2a-451b-9efa-f037124c3519/Untitled.png)

이미지 출저 : cloudFlare

### TLS Handshake 발생

TLS Handshake는 사용자가 HTTPS를 통해 웹사이트를 탐색하고 브라우저가 처음 해당 웹사이트의 원본 서버를 쿼리하기 시작할 때 마다 발생. TLS Handshake는 TCP연결이 TCP handshake 를 통해 열린 이후에 발생함

TLS Handshake가 발생하게 되면

1. 사용할 TLS 버전 지정 (TLS 1.0, 1.2, 1.3 등)
2. 사용할 암호 제품군 결정
3. 서버의 공개키와 SSL인증서 기관의 디지털 서명을 통해 서버의 ID 인증
4. 핸드셰이크가 완료된 후에 대칭 암호화를 사용하기 위한 세션 키 생성

### TLS Handshake 과정

TLS Handshake는 클라리언트와 서버가 교환하는 일련의 메시지

TLS Handshake의 정확한 단계는 사용되는 키 교환 알고리즘의 유형과 커뮤니케이션에 따라 달라지지만 **보통 RSA 키 교환 알고리즘**을 쓴다.

1. `'client hello'` 메시지 

클라이언트가 서버로 'hello' 메시지를 전송하면서 handshake가 시작됨
메시지에 클라이언트가 지원하는 TLS 버전, 지원되는 암호 제품군, `'client random'`이라고 하는 무작위 바이트 문자열이 포함되어 전달
2. `'server hello'`
`'client hello'` 의 응답으로 서버가 서버의 `SSL 인증서` , 서버에서 선택한 암호군, `'server random'` 을 포함하여 전달

3. 인증
클라이언트가 서버의 SSL 인증서를 인증서 발행 기관을 통해 검증하여 서버가 실제 해당 도메인의 소유자인지 확인

4. `premaster secret`
클라이언트 측에서 `premaster secret` 라고 하는 무작위 바이트 문자열을 하나 더 전송함

5. 개인 키 사용
서버가 `premaster secret` 을 해독
** `premaster secret` : 공개키로 암호화 되어 서버가 개인키로만 해독할 수 있음

6. 세션 키 생성
클라이언트와 서버가 모두 `client random` , `server random` ,`premaster secret`  을 사용하여 세션키를 생성

7. 서버 준비 완료
서버측에서 세션키로 암호화된 `finished` 메시지를 전송

8. 암호화 성공
handshake 완료. 세션키를 이용하여 커뮤니케이션을 계속 진행

---

References

[https://www.cloudflare.com/ko-kr/learning/ssl/what-happens-in-a-tls-handshake/](https://www.cloudflare.com/ko-kr/learning/ssl/what-happens-in-a-tls-handshake/)

[http://wiki.gurubee.net/display/SWDEV/SSL+(TLS)](http://wiki.gurubee.net/display/SWDEV/SSL+%28TLS%29)
