[CS-/임계영역.md at main · yunghun97/CS- (github.com)](https://github.com/yunghun97/CS-/blob/main/OS/%EC%9E%84%EA%B3%84%EC%98%81%EC%97%AD.md)

# 임계영역(Critical Section)

## <span style="color:white">개념</span>

- ### 프로세스간에 공유자원을 접근하는데 있어서 문제가 발생하지 않도록 한번에 하나의 프로세스만 이용하게끔 보장해줘야 하는 영역

![임계영역동기화문제](https://user-images.githubusercontent.com/71022555/145226486-c53f2ae1-5421-4bd5-ac5d-e5873ba86a13.png)

## 해결방법

1. 락(LOCK)

2. 뮤텍스(Mutex)

3. 세마포어(semaphore)

4. 모니터(monitor)

---

## <span style= "color:lightBlue">락(LOCK)</span>

### <br> 하나의 프로세스가 자원을 사용하고 있는 동안에는 잠궈서 접근을 못하게 하는 방식

### <br> ex) A 스레드가 공유자원 사용 시 Lock 설정 B가 공유자원 접근 요청 시 Lock이 걸려있으면 해제 할 때 까지 대기

![임계영역동기화LOCK](https://user-images.githubusercontent.com/71022555/145226470-a12226ec-ae9c-4ec4-90e8-6718e71cbca2.png)

## <br> 락(Lock)의 문제점

- ### 특정한 상황에서 제대로 작동하지 않는 문제 발생

## <br> 락(Lock)의 해결방안

1. ### 소프트웨어 알고리즘(ex\_피터슨 알고리즘(느려서 사용X))
2. ### 더 이상 쪼개지지않는 하드웨어 명령어로 구현하는 방법
3. ### 인터럽트를 disable하고 enable하는 방법
<br>
<br>

---

</br>

## <span style= "color:lightBlue">Mutex</span>

### 0과 1을 가진 이진 세마포어와 유사.

### 다른 프로세스간의 동기화를 할 때 사용한다.

<br>

## <span style= "color:lightGreen">Lock과 Mutex차이점</span>

- ### 락(LOCK) 락이 걸려 있을 경우 이를 얻을 때까지 무한 로프를 돌면서 CPU를 점유하고 있다.
- ### 뮤텍스(Mutex)는 락이 걸려 있을 경우 락이 풀릴 때까지 기다리며 컨텍스트 스위칭을 실행한다.

### (단시간에 자원을 얻을 수 있는 경우 컨텍스트 스위칭을 하는 과정이 자원을 더 소모할 수도 있다.)

### 컨텍스트 스위칭(Context Switching) 기존의 프로세스의 상태 또는 레지스터 값을 저장하고 CPU가 다음 프로세스를 수행하도록 새로운 프로세스의 상태 또는 레지스터 값(Context)를 교체하는 작업

---

</br>

## <span style= "color:lightBlue">세마포어</span>

### 락(스핀락) 뮤텍스와는 다르게 표현형이 정수형이며 정수형이기 때문에 하나 이상의 컴포넌트가 공유자원에 접근하도록 허용할 수 있다.

1. ### 이진 세마포어
   - 1개의 자원을 Locking하는 기법
   - 쓰레드가 자원을 사용 시 Lock, 만납시 Unlock (Lock : 0, Unlock 1)
2. ### 카운팅 세마포어
   - 공유된 자원의 개수를 의미한다.
   - 0이면 공유된 자원(사용 중인 자원이 없다.)
   - 공유된 자원이 5개면 5 -> 4 -> 3 -> 2 -> 1 -> 0 순으로 감소된다.

---

<br>

## <span style= "color:lightBlue">모니터</span>

### 한 프로세스 내에 있는 하나의 스레드만 자원에 접근 가능하다.

### 뮤텍스와 같은 원리로 작동

<br>

## <span style= "color:lightGreen">뮤텍스와 차이점</span>

<br>

### 뮤텍스

1. 다른 프로세스(애플리케이션)간에 동기화할 때 사용할 수있다.
2. 보통 운영체제 커널, 프레임워크, 라이브러리에 의해서 제공된다.
3. 무겁고 느리다.

### 모니터

1. 하나의 프로세스(애플리케이션)내에 다른 스레드 간에 동기화할 때 사용한다.
2. 주로 프레임워크나 라이브러리 그 자체에서 제공된다.
3. 가볍고 빠르다.
4. Java에서 모니터를 모든 객체에서 기본적으로 제공하지만 C에서는 모니터를 사용할 수 없다.
