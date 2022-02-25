# TCP 흐름 제어,혼잡 제어

---

# Congestion(혼잡)

네트워크 계층에서, 메시지 트래픽이 많아 네트워크 응답 시간이 느려지는 상태

### Effect of Congestion

1. delay가 증가하면 성능이 저하된다
2. delay가 증가하면 retransmission이 발생하여 상황 악화

### Congestion Control Algorithm

1. Leaky Bucket Algorithm

![Untitled](TCP%20%E1%84%92%E1%85%B3%E1%84%85%E1%85%B3%E1%86%B7%20%204c438/Untitled.png)

깔대기라는 버퍼를 사용하여 송신 호스트에서 나오는 데이터의 가변율을 고정율로 협상하여 **일정한 전송률을 가지게 만들어 트레픽을 줄이는 알고리즘**이다.

### 2. Token Bucket Algorithm

토큰 버킷 알고리즘의 필요성

리키 버킷 알고리즘은 트래픽량에 관계없이 평균 속도로 출력 패턴을 적용하기 때문에, 버스트 트래픽을 처리하려면 데이터가 손실되지 않도록 유연한 알고리즘이 필요하다

항상 정해진 일정량만 통과하도록 되어 있는 Leaky Bucket과는 달리 **트래픽이 버스트 한 경우에도 정해진 한계치 범위 내에서는 통과 가능**

![Untitled](TCP%20%E1%84%92%E1%85%B3%E1%84%85%E1%85%B3%E1%86%B7%20%204c438/Untitled%201.png)

- Buket 자체를 FIFO 큐로 사용하지 않고, 트래픽을 제어하기 위한 제어용 토큰을 관리하는 용도로 사용
- 트래픽은 토큰의 유무에 따라 흐름의 제어를 받게 됨
- M * s = C + ρ * s
    
     S – time taken
    
    M – Maximum output rate
    
    ρ – Token arrival rate
    
    C – Capacity of the token bucket in byte
    

### Congestion 관련 연습 문제

1. Application 계층에서 TCP 계층에 전달 할 수 있는 최대 데이터 크기
답: 모든 크기
정의된 제한은 없으며, 하위 계층은 필요한 경우 데이터를 나누어서 전송한다
2. 토큰 버킷으로 인해 10Mbps 네트워크로 규정된 컴퓨터에서, 토큰 버킷이 2Mbps rate으로 채워지며, 초기에 16메가바이트 용량으로 채워질 때, 10Mbps에서 전송할 수 있는 최대 시간은?
    
    ```
    토큰 버킷의 용량 (b) = 16 Mbits
    최대 전송률(M) = 10Mbps
    최대 시간 = b/(M-r) = 16/(10-2) = 2 seconds
    ```
    

# TCP 혼잡 제어

송신측의 데이터 전달과 네트워크의 데이터 처리 속도 차이를 해결하기 위한 기법

### TCP의 혼잡 제어 알고리즘

1. AIMD (Addictive Increase / Multicative Decresase)
    
    ![Untitled](TCP%20%E1%84%92%E1%85%B3%E1%84%85%E1%85%B3%E1%86%B7%20%204c438/Untitled%202.png)
    
    - 처음에 패킷을 하나씩 보내고 문제없이 도착하면 윈도우의 크기를 1씩 증가시켜가며 전송한다.
    - 만약 전송에 실패하면 윈도우 크기를 반으로 줄인다.
    - 윈도우 크기를 너무 조금씩 늘리기 때문에 네트워크의 모든 대역을 활용하여 제대로 된 속도로 통신하기까지 시간이 오래 걸린다.
2. 슬로우 스타트 (Slow Start)
    
    ![Untitled](TCP%20%E1%84%92%E1%85%B3%E1%84%85%E1%85%B3%E1%86%B7%20%204c438/Untitled%203.png)
    
    - 윈도우의 크기를 1, 2, 4, 8... 과 같이 2배씩 증가시킨다.
    - 혼잡이 감지되면 윈도우 크기를 1로 줄여버린다.
    - 시간이 지날수록 `AIMD` 보다 빠르게 윈도우 크기를 증가시킨다
    
    ![Untitled](TCP%20%E1%84%92%E1%85%B3%E1%84%85%E1%85%B3%E1%86%B7%20%204c438/Untitled%204.png)
    
    Threshold: 여기까지만 slow start를 사용하겠다는 표시. 윈도우 크기를 지수적으로 증가시키다보면 크기가 기하급수적으로 늘어나 전송 데이터의 크기가 제어가 힘들어져 threshold에 도달하면 1씩 윈도우 증가
    
3. 빠른 재전송 (Fast Retransmit)
    
    패킷을 받는 수신자 입장에서는 세그먼트로 분할된 내용들이 순서대로 도착하지 않는 경우가 생길 수 있다.
    
    ![Untitled](TCP%20%E1%84%92%E1%85%B3%E1%84%85%E1%85%B3%E1%86%B7%20%204c438/Untitled%205.png)
    
    위 예제에서, segments 1~7 이 순차적으로 도착해야 하지만 seg4 packet이 제대로 전송되지 않았다. Receiver 측에서는, segment가 도착한 순서대로 ack 를 보내기 때문에, seg 1~3 을 정상적으로 받았을 때 ack 1~3을 전송하지만 seg4 가 도착하지 않았기 때문에 더이상 ack 를 보내지 않고 sender 측의 송신이 끝난 후에 seg4가 도착하지 않았음을 알린다.
    
    1. 빠른 회복 (Fast Recovery)
        
        빠른 회복은 혼잡한 상태가 되면 윈도우 크기를 1로 줄이지 않고 반으로 줄이고 선형증가시키는 방법이다. 이 방법을 적용하면 혼잡 상황을 한번 겪고 나서부터는 AIMD 방식으로 동작한다.
        

### TCP 혼잡 제어 정책

1. TCP Tahoe
    
    TCP Tahoe는 처음에는 Slow Start를 사용하다가 threshold에 도달하면 AIMD 방식을 사용한다. 그러다가 3 ACK Duplicated 또는 타임아웃이 발생하면 혼잡이라고 판단하여 임계점은 혼잡이 발생한 윈도우 크기의 절반으로, 윈도우 크기는 1로 줄인다.
    
    ![Untitled](TCP%20%E1%84%92%E1%85%B3%E1%84%85%E1%85%B3%E1%86%B7%20%204c438/Untitled%206.png)
    
    하지만, 혼잡 판단 이후 Slow Start 구간에서 윈도우 크기를 키울 때 1부터 다시 키워나가야하기 때문에 TCP Reno 방식이 등장했다.
    
2. TCP Reno
    
    TCP Tahoe는 처음에는 Slow Start를 사용하다가 threshold에 도달하면 AIMD 방식을 사용한다. 하지만  Tahoe 방식과는 다르게 3 ACK Duplicated와 Timeout을 구분하여, 3 ACK Duplicated일 경우 빠른 회복 방식을 사용한다.
    
    즉, 윈도우 크기를 1로 줄이는 것이 아니라 반으로 줄이고 윈도우 크기를 선형적으로 증가시킨다. 그리고 threshold를 줄어든 윈도우 값으로 설정한다.
    

# TCP 흐름 제어

송신측과 수신측의 데이터 처리 속도 차이를 해결하기 위한 기법

Sender의 속도가 Receiver의 속도보다 빠를 때, 데이터 손실이 발생할 수 있다. 또한, 데이터 손실이 발생함에 따라 불필요한 응답과 데이터 재전송이 발생하게 된다. 따라서, sender의 데이터 전송량을 receiver의 데이터 수신량에 따라 조절해야한다

### TCP의 흐름제어 알고리즘

1. Stop and Wait 방식
    
    매번 전송한 패킷에 대해 확인 응답을 받은 후에 다음 패킷을 전송
    

![Untitled](TCP%20%E1%84%92%E1%85%B3%E1%84%85%E1%85%B3%E1%86%B7%20%204c438/Untitled%207.png)

1. Sliding Window 방식
    
    receiver에서 설정한 윈도우 크기만큼 sender에서 확인응답 없이 세그먼트를 전송할 수 있게 하여 데이터 흐름을 동적으로 조절하는 제어 기법
    
    먼저, 윈도우에 포함되는 모든 페킷을 전송하고 그 패킷들의 전달이 확인되는대로 이 윈도우를 옆으로 슬라이딩하고 다음 패킷을 전송
    
    <aside>
    📌 윈도우 : TCP/IP를 사용하는 모든 호스트들은 송신과 수신을 위해 2개의 윈도우를 가지고 있는데, 호스트들은 실제 데이터를 보내기 전에 3 way handshaking을 통해 receiver의 윈도우 사이즈를 자신의 send window사이즈를 맞추게 된다.
    
    </aside>
    
    ![Untitled](TCP%20%E1%84%92%E1%85%B3%E1%84%85%E1%85%B3%E1%86%B7%20%204c438/Untitled%208.png)
    
    세부 구조
    
    1. Sender Buffer
        
        ![203-211: 아직 전송 x | 200-202: 전송됨. 확인응답 x | -200: 전송+확인응답 수신](TCP%20%E1%84%92%E1%85%B3%E1%84%85%E1%85%B3%E1%86%B7%20%204c438/Untitled%209.png)
        
        203-211: 아직 전송 x | 200-202: 전송됨. 확인응답 x | -200: 전송+확인응답 수신
        
    2. Receiver Window
        
        ![Untitled](TCP%20%E1%84%92%E1%85%B3%E1%84%85%E1%85%B3%E1%86%B7%20%204c438/Untitled%2010.png)
        
    3. Sender Window
        
        ![Untitled](TCP%20%E1%84%92%E1%85%B3%E1%84%85%E1%85%B3%E1%86%B7%20%204c438/Untitled%2011.png)
        
        sender window를 receiver보다 작거나 같은 크기로 지정하여 흐름제어
        
    4. Sender Window - Slides
        
        ![Before: 20- ~ 204 전송→ sender에서 확인 응답응 보내고, 203~209 범위로 이동(slides)
        After: 205~209가 전송 가능한 상태](TCP%20%E1%84%92%E1%85%B3%E1%84%85%E1%85%B3%E1%86%B7%20%204c438/Untitled%2012.png)
        
        Before: 20- ~ 204 전송→ sender에서 확인 응답응 보내고, 203~209 범위로 이동(slides)
        After: 205~209가 전송 가능한 상태
        
    5. Selected Repeats