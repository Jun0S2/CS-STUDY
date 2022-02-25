# WebSocket

[https://velog.io/@oyeon/웹-소켓WebSocket](https://velog.io/@oyeon/%EC%9B%B9-%EC%86%8C%EC%BC%93WebSocket)

## 웹 소켓이란?

![image](https://user-images.githubusercontent.com/71022555/145073871-ba4b0e42-08e5-4721-b005-57cbf727c485.png)
<br>

- ### 웹 소켓이란 두 프로그램 간의 메시지를 교환하기 위한 통신 방법 중 하나이다.
- ### W3C와 IETF에 의해 자리잡은 표준 프로토콜 중 하나
  - W3C : www(world wide web)을 위한 표준을 개발하고 장려하는 조직
  - IETF : 인터넷의 운영, 관리, 개발에 대해 협의하고 프로토콜과 구조적인 사안들을 분석하는 인터넷 표준화 작업 기구
- ### 현재 인터넷 환경(HTML5)에서 많이 사용된다.
- ### 웹 소켓을 지원하는 브라우저의 경우 웹 소켓 프로토콜을 지원한다.
  - 구글 크롬, 마이크로소프트 에지, 인터넷 익스플로러, 파이어폭스, 사파리, 오페라 등 대부분의 브라우저가 이 프로토콜을 지원

<br>

---

## 웹 소켓의 특징

### 1. 양방향 통신(Full-Duplex)

- 데이터 송수신을 동시에 처리할 수 있는 통신 방법
- 클라이언트와 서버가 서로에게 원할 때 데이터를 주고 받을 수 있다.
- 통상적인 HTTP 통신은 Client가 요청을 보내는 경우에만 Server가 응답하는 단방향 통신
  <br>

### 2. 실시간 네트워킹(Real Time-Networking)

- 웹 환경에서 연속된 데이터를 빠르게 노출
- Ex) 채팅, 주식, 비디오 데이터
- 여러 단말기에 빠르게 데이터를 교환
  <br>

---

## 웹 소켓 이전의 실시간 통신

### 1. Polling

![image](https://user-images.githubusercontent.com/71022555/145074102-3aacb765-bb7f-4d51-8802-da9620abb55e.png)
<br>

- ### 서버로 일정 주기 요청 송신
- ### real-time 통신에서는 언제 통신이 발생할지 예측이 불가능하기 때문에 불필요하더라도 일정주기로 request와 connection을 생성
- ### Real Time 통신이라고 부르기 애매할 정도의 실시간성
<br>

### 2. Long polling

![image](https://user-images.githubusercontent.com/71022555/145074178-5eb6ab0b-8f57-41fd-9748-7f7813005f2a.png)
<br>

- ### 서버에 요청을 보내고 이벤트가 생겨 응답을 받을 때까지 연결 종료 X
- ### 응답을 받으면 끊고 재요청
- ### But, 많은 양의 메세지가 쏟아질 경우 polling과 같다.
<br>

### 3. Streaming

![image](https://user-images.githubusercontent.com/71022555/145074243-92e8d33e-dae1-46bc-8466-8f4bb4b3f67c.png)
<br>

- ### 서버에 요청을 보내고 끊기지 않은 연결상태에서 끊임없이 데이터를 수신
- ### 클라이언트에서 서버로의 데이터 송신이 어렵다.
  결과적으로 이 모든 방법이 HTTP를 통해 통신하기 때문에 Request, Response 둘 다 Header가 불필요하게 큼
  <br>

---

## 웹 소켓 동작 방법

## 1. 핸드 쉐이킹

### 1) 클라이언트 요청

![image](https://user-images.githubusercontent.com/71022555/145074309-153bb09d-a2d2-4504-bbff-f04df77179ad.png)

```
GET /chat HTTP/1.1
Host: server.example.com
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Key: x3JJHMbDL1EzLkh9GBhXDw==
Sec-WebSocket-Protocol: chat, superchat
Sec-WebSocket-Version: 13
Origin: http://example.com
```

```
GET /chat HTTP/1.1
```

- ### 반드시 GET 메서드를 사용
- ### 연결 수립 과정은 HTTP 프로토콜 사용
- ### HTTP 버전은 1.1 이상
<br>

```
Host: server.example.com
```

- ### 웹소켓 서버의 주소
<br>

```
Upgrade: websocket
```

- ### 현재 클라이언트, 서버, 전송 프로토콜 연결에서 다른 프로토콜로 업그레이드 또는 변경하기 위한 규칙
- ### 따라서, Upgrade: websocket의 경우 websocket 프로토콜로 변경하겠다는 의미
<br>

```
Connection: Upgrade
```

- ### Upgrade 헤더 필드가 명시되었을 경우, 송신자는 반드시 Upgrade 옵션을 지정한 Connection 헤더 필드로 전송
<br>

```
Sec-WebSocket-Key: x3JJHMbDL1EzLkh9GBhXDw==
```

- ### 길이가 16바이트인 임의로 선택된 숫자를 base64로 인코딩한 값
- ### Clinet와 Server간의 신원을 인증
<br>

```
Sec-WebSocket-Protocol: chat, superchat
```

- ### 클라이언트가 요청하는 여러 서브 프로토콜을 의미
- ### 공백문자로 구분되며 순서에 따라 우선권이 부여
- ### 서버에서 여러 프로토콜 혹은 프로토콜 버전을 나눠서 서비스할 경우 필요한 정보
<br>

```
Origin: http://example.com
```

- ### 클라이언트의 주소
- ### 클라이언트로 웹 브라우저를 사용하는 경우 필수항목
<br>

### 2) 서버 응답

![image](https://user-images.githubusercontent.com/71022555/145074617-8fee98b9-9ef0-46e2-9996-84e90e70b38c.png)

```
HTTP/1.1 101 Switching Protocols
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Accept: HSmrc0sMlYUkAGmm5OPpG2HaGWk=
Sec-WebSocket-Protocol: chat
```

<br>

```
HTTP/1.1 101 Switching Protocols
```

- ### 101 Switching Protocols가 Response로 오면 웹소켓이 연결
<br>

```
Sec-WebSocket-Accept: HSmrc0sMlYUkAGmm5OPpG2HaGWk=
```

- ### 클라이언트로부터 받은 Sec-WebSocket-Key를 사용하여 계산된 값
- ### 이 값이 클라이언트에서 계산한 값과 일치하지 않으면 연결 수립 X
<br>

## 2. 데이터 전송

![image](https://user-images.githubusercontent.com/71022555/145074849-7572ad81-40e7-440c-9780-c4978c613785.png)
<br>

- ### 프로토콜이 ws로 변경
- ### wss(443) : 데이터 보안을 위해서 SSL을 적용한 프로토콜
- ### Message : 여러 frame이 모여서 구성하는 하나의 메시지 단위
- ### frame : communication에서 가장 작은 단위의 데이터, 작은 헤더 + payload로 구성
  - cf) payload : 전송되는 데이터 자체를 의미한다.(헤더, 메타데이터, 에러 체크 비트 등을 제외한 부분)
- ### 웹소켓 통신에 사용되는 데이터는 UTF-8 인코딩
      - Ex) 0x00 (보내고 싶은 데이터) 0xff
  <br>

### frame 헤더 구조

![image](https://user-images.githubusercontent.com/71022555/145074958-25c33140-a3f5-48c2-9b28-297a95972e5d.png)
<br>

### END : 이 프레임이 전체 메시지의 끝인지 나타내는 플래그

### RSV : 프로토콜별로 사용할 수도 있고, 아닐 수도 있다.

Opcode

- ### Continue (0x0) : 전체 메시지의 일부임을 의미
- ### Text (0x1) : 포함된 데이터가 UTF8 텍스트라는 의미
- ### Binary (0x2) : 포함된 데이터가 이진 데이터라는 의미
- ### Close (0x8) : Close 핸드쉐이크를 시작한다는 의미

### Length : 이 프레임에 포함된 데이터의 총 길이를 나타내는 단위

![image](https://user-images.githubusercontent.com/71022555/145075063-21c29a05-d5b1-4d5a-b584-e35094ae4df2.png)
<br>

### 간단 정리

![image](https://user-images.githubusercontent.com/71022555/145075102-1ac21d92-9a3a-4725-b398-57f3d7b01383.png)
<br>

## 웹 소켓 프로토콜의 특징

### - 최초 접속에서만 http 프로토콜 위에서 handshaking을 하기 때문에 http header를 사용한다.

### - 웹 소켓을 위한 별도의 포트는 없으며, 기존 포트(http-80, https-443)을 사용

### - 프레임으로 구성된 메시지라는 논리적 단위로 송수신

### - 메시지에 포함될 수 있는 교환 가능한 메시지는 텍스트와 바이너리 뿐이다.

<br>

## 웹 소켓 한계

## HTML5 이전의 기술로 구현된 서비스에서는?

<br>

### SockJS, Socket io

- ### HTML5 이전의 기술로 구현된 서비스에서 웹 소켓처럼 사용할 수 있도록 도와주는 기술
- ### Javascript를 이용하여 브라우저 종류에 상관없이 실시간 웹을 구현
- ### WebSocket, FlashSocket, AJAX Long Polling, AJAX Multi part Streaming, IFrame, JSONP Polling을 하나의 API로 추상화
- ### 즉, 브라우저와 웹 서버의 종류와 버전을 파악하여 가장 적합한 기술을 선택하여 사용하는 방식
<br>

### 형식이 정해지지 않아 생기는 문제

- ### WebSocket은 문자열들을 주고 받을 수 있게 해줄 뿐 그 이상의 일을 하지 않는다.
- ### 주고 받는 문자열의 해독은 온전히 어플리케이션에 맡긴다.
- ### HTTP의 경우 형식을 정해주었기 때문에 모두가 약속을 따르기만 하면 해석할 수 있다.
- ### But, WebSocket은 형식이 정해져 있지 않기 때문에 어플리케이션에서 쉽게 해석하기 힘들다.
- ### 따라서, WebSocket을 사용할 때 sub-protocols을 사용해서 주고 받는 메시지의 형태를 약속하는 경우가 많다.
      - Ex) STOMP
  <br>

### STOMP(Simple Text Oriented Message Protocol)

- ### 채팅 통신을 하기위한 형식을 정의
- ### HTTP와 유사하게 간단히 정의되어 해석하기 편한 프로토콜
- ### 일반적으로 웹 소켓 위에서 사용
<br>

### STOMP 프레임 구조

![image](https://user-images.githubusercontent.com/71022555/145075327-943747c3-cb1a-4658-869d-81688f7449f7.png)
<br>

- ### 프레임 기반의 프로토콜이다. 프레임은 명령, 헤더, 바디로 구성된다.
- ### 자주 사용되는 명령은 CONNECT, SEND, SUBSCRIBE, DISCONNECT 등이 있다.
- ### 헤더와 바디는 빈 라인으로 구분하며, 바디의 끝은 NULL 문자로 설정한다.

```
reference
https://ko.wikipedia.org/wiki/%EC%9B%B9%EC%86%8C%EC%BC%93
https://d2.naver.com/helloworld/1336
https://www.youtube.com/watch?v=MPQHvwPxDUw
https://wondongho.tistory.com/69
https://skout90.github.io/2017/08/15/Web/%EC%86%8C%EC%BC%93%EC%9D%B4%EB%9E%80/
https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=scw0531&logNo=221097188275
```
