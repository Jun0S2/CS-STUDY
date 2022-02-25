# OSI 7 Layer

[https://velog.io/@oyeon/OSI-7-Layer](https://velog.io/@oyeon/OSI-7-Layer)

# 네트워크 개념

## 1. 네트워크의 구성 형태

![image](https://user-images.githubusercontent.com/71022555/145221778-3c0a46f3-b1d9-4368-ae86-14752eed1658.png)
<br>

### Mesh Topology (망형)

- 컴퓨터와 컴퓨터마다 전선을 두는 방식은 통신하려는 컴퓨터가 많아질수록 비용면에서 비효율적
- 따라서, 전선 하나를 가지고 여러 컴퓨터와 통신할 방법을 모색해야 한다.
  <br>

### Bus Topology (버스형)

- Bus Topology 형태의 전기가 통하는 구리 선에 여러 대의 컴퓨터가 연결되었다고 가정해보자.
- 한 컴퓨터에서 다른 컴퓨터로 0010 0100 데이터를 보내고 싶다면, 0010 0100에 해당하는 전자기파를 구리 선으로 흘려보낸다.
- 구리 선은 전기가 통하므로, 신호는 구리 선의 모든 곳으로 전달되어 모든 컴퓨터에 전달된다.
- 원하는 컴퓨터에 전송하는 데 성공했지만, 다른 컴퓨터도 데이터를 받았다.
  <br>

### Star Topology (성형)

- 허브를 중심으로 컴퓨터들이 연결된 구조
  <br>

---

## 2. 허브 vs 스위치 vs 라우터

### 더비 허브 (허브)

- 한 컴퓨터에서 다른 컴퓨터로 데이터를 보낼 때, 다른 컴퓨터도 메시지를 읽을 수 있다.
- Collision Domain(충돌 영역)을 나누지 못하고 한 PC가 = - - BroadCast를 뿌리게 되면,
- 허브에 연결된 모든 PC, Server들은 BroadCast 패킷을 받게 된다.
- 이 경우 허브에 연결된 모든 네트워크에서는 충돌이 발생할 수 있으며, 속도가 저하된다.
  <br>

### 스위칭 허브 (스위치)

- 메시지의 목적을 확인해서 특정 컴퓨터에만 메시지를 전달할 수 있다.
- 각 Port 별로 Bandwidth를 제공하며 Switch는 자기에게 주어진 PC, Server들의 MAC 주소를 저장.
- Collision Domain(충돌 영역)을 나눌 수 있다.
  <br>

### 라우터

- 스위치와 스위치를 연결해서 서로 다른 네트워크에 속한 컴퓨터끼리 통신이 가능하게 해주는 장비
- 라우터가 스위치 역할까지 하는 경우도 있다. ex. 가정용 무선 라우터
  <br>

### 허브 vs 스위치

- 허브는 연결된 기기 중 하나에서 전송된 패킷이 허브에 연결된 모든 기기로 브로드캐스팅 된다.
- 스위치는 패킷의 목적지 주소로 지정된 기기로 이어지는 포트로만 패킷이 전달된다.
  <br>

### 스위치 vs 라우터

- 라우터는 계층 3(네트워크 계층)에서 작동하며 네트워크를 다른 네트워크로 연결하는 데 사용
- 스위치를 LAN에서 사용되는 것, 라우터를 WAN에서 사용되는 것으로 이해하면 쉽다.
  <br>

---

## TCP/IP Updated Layer

![image](https://user-images.githubusercontent.com/71022555/145224100-568274b6-fa9a-4c35-a4b8-fda8520cc60c.png)

- 현재 인터넷에서 사용하는 TCP/IP updated 모델을 중심으로 알아보자.
  <br>

## 1. Physical Layer

- ### 0과 1의 나열을 아날로그 신호로 바꾸어 전선으로 흘려보내고(Encoding)
- ### 아날로그 신호가 들어오면 0과 1의 나열로 해석하여(Decoding)
- ### 물리적으로 연결된 두 대의 컴퓨터가 0과 1의 나열을 주고받을 수 있게 해주는 모듈(Module)

## 2. Data-link Layer

- ### 같은 네트워크에 있는 여러 대의 컴퓨터들이 데이터를 주고받는 데 필요한 모듈
- ### 2계층 Encoder는 들어온 Data에 Framing 처리를 한다.

### Framing

- ### Data-link Layer에 속하는 작업 중 하나이다.
- ### 한 컴퓨터에 여러 데이터가 들어올 때, 이를 구분하려는 방법
- ### Ex. 송신자가 데이터를 보낼 때 데이터 시작 부분에 1111, 데이터 마지막 부분에 0000을 붙인다.
- ### 이렇게 데이터들을 감싸서 보내면, 수신자가 여러 데이터를 받더라도 그 데이터를 구분할 수 있다.

## 3. Network Layer

- ### 수많은 네트워크의 연결로 이루어지는 inter-network 속에서
- ### 어딘가에 있는 목적지 컴퓨터로 데이터를 전송하기 위해
- ### IP 주소를 이용해서 길을 찾고 (routing)
- ### 자신 다음의 라우터에 데이터를 넘겨주는 것 (forwarding) 층 Encoder에 들어간다.
- ### 3계층 Encoder는 들어온 Data의 앞에 목적지 IP 주소를 추가시켜준다.

## 1계층~3계층 과정 정리

![image](https://user-images.githubusercontent.com/71022555/145224316-5c2df500-e85e-4d92-95c4-e2537ace5ded.png)

### 용어

- 패킷 : 목적지 IP 주소 + Data로 이루어진 구조체
- Framing : Data-link Layer 설명 참고

### Data를 보내는 컴퓨터

### 3 → 2

- Data를 보내는 컴퓨터의 Data가 들어오면, 3계층 Encoder에서 패킷을 만들어 2계층에 전송

### 2 → 1

- 3계층에서 패킷이 들어오면, 2계층 Encoder에서 패킷을 Framing을 통해 감싸 1계층에 전송

### 1 → 1

- 2계층에서 Framing에 감싸진 패킷이 들어오면, 1계층 Encoder가 아날로그 신호로 바꿔 인접한 라우터에 흘려보낸다.
- 인접한 라우터에 아날로그 신호가 들어온다.

### 라우터

### 1 → 2

- 들어온 아날로그 신호를 1계층 Decoder를 통해 0과 1로 해석한다. 이를 통해 얻은 Framing으로 감싸진 패킷을 2계층으로 보낸다.

### 2 → 3

- 1계층에서 Framing으로 감싸진 패킷이 들어오면, 2계층 Decoder를 통해 Framing(0000, 1111)을 제거한다. 이후 패킷을 3계층에 전송

### 3 → 3

- 2계층에서 패킷이 들어오면, 3계층 Decoder를 통해 목적지 IP 주소가 사용되고
- 다시 3계층 Encoder로 들어간다.

### 3 → 2

- 들어온 Data를 3계층 Encoder를 통해 패킷을 만들어 2계층에 전송

### 2 → 1

- 3계층에서 패킷이 들어오면, 2계층 Encoder에서 패킷을 Framing을 통해 감싸 1계층에 전송

### 1 → 1

- 다음 순서 라우터에 전달.

위에 작성한 라우터에서 일어나는 일(라우팅 과정) 반복

## 4. Transport Layer

![image](https://user-images.githubusercontent.com/71022555/145224682-dbe99314-c351-43f2-b71f-9407f1bd69df.png)

- ### 포트 번호를 사용하여 도착지 컴퓨터의 최종 도착지인 프로세스까지 데이터가 도달하게 하는 모듈
- ### 데이터를 받고자 하는 프로세스들은 포트 번호를 가져야 한다.
- ### 4계층 Encoder는 들어온 Data의 앞에 포트 번호를 추가시켜준다.

## 5. Application Layer

![image](https://user-images.githubusercontent.com/71022555/145224707-e9c79bf3-5608-4b8b-bab9-389a6ab4e7c3.png)

### TCP/IP 소켓 프로그래밍

- ### 운영체제의 Transport layer에서 제공하는 API를 활용해서 통신 가능한 프로그램을 만드는 것을 TCP/IP 소켓 프로그래밍, 또는 네트워크 프로그래밍이라고 한다.
- ### 소켓 프로그래밍만으로도 클라이언트, 서버 프로그램을 따로 만들어 동작시킬 수 있다.
- ### TCP/IP 소켓 프로그래밍을 통해 자신만의 Application Layer 인코더와 디코더를 만들 수 있다. 즉, Application Layer 프로토콜을 만들어서 사용할 수 있다.
- ### 대표적인 Application Layer 프로토콜인 HTTP로 인코딩, 디코딩을 살펴보자.

## 마무리

- ### 네트워크 시스템은 Layerd Architecture를 따르는 대표적인 예시로써, 하나의 거대한 소프트웨어라고 할 수 있다.
- ### 결국, OSI 7 Layers 모델은 거대한 네트워크 소프트웨어의 구조를 설명한다.
<br>

---

### 📺 reference

https://www.youtube.com/watch?v=1pfTxp25MA8

https://mslee89.tistory.com/49

https://velog.io/@amuse/OSI-7-Layers

https://www.itworld.co.kr/news/167585

https://levelup-teddybear.tistory.com/19

https://security-nanglam.tistory.com/176

http://ko.rfidctek.com/news/difference-between-analog-and-digital-signals-21014371.html
