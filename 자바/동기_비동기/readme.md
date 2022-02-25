# [Java] Blocking/ Non-blocking , 
Sync / Async

동기 vs 비동기 (Sync vs Async ) : **처리해야할 작업들을 어떠한 흐름으로 처리할 것인가**에 대한 관점

블로킹 vs 논블로킹 : 처리되어야 하는 작업이, **전체적인 작업 흐름을 막느냐 안막느냐**에 대한 관점

# Sync vs Async

![출처 - [https://poiemaweb.com/js-async](https://poiemaweb.com/js-async) - 동기 & 비동기는 은행 업무 예시로 가장 많이 비유된다.](%5BJava%5D%20Blo%2092ea1/Untitled.png)

출처 - [https://poiemaweb.com/js-async](https://poiemaweb.com/js-async) - 동기 & 비동기는 은행 업무 예시로 가장 많이 비유된다.

- 동기 : 은행 업무를 한줄로 서서 순서대로 업무로 진행
- 비동기 : 여러 업부창에서 일을 분업해서 진행

## Sync (동기)

동기 작업은 테스크를 순차적으로 실행되며, 어떤 작업이 수행중이면 다음 작업은 대기상태가 된다

```java
public class Sync{
	public static void main(String[] args){
		method1();
		method2();
		method3();
	}
	public static void method1(){System.out.println("method 1 ");}
	public static void method2(){System.out.println("method 2 ");}
	public static void method3(){System.out.println("method 3 ");}
}
```

자바는 위에서 아래로 코드를 해석하여 main내의 순으로 프로그램이 실행되기 떄문에, 프로그램을 몇번을 실행해도 method call의 순서는 변하지 않는다.

![Untitled](%5BJava%5D%20Blo%2092ea1/Untitled%201.png)

## Async (비동기)

비동기 작업은 테스크를 병렬적으로 수행하여, 테스크가 종료되지 않은 상태라도 대기하지 않고 다음 테스크를 실행한다.

```java
public class Async{
	public static void main(String[] args) {
		Thread t1 = new Thread(()->{ method1();});
		Thread t2 = new Thread(()->{ method2();});
		Thread t3 = new Thread(()->{ method3(); });	
		t1.start();
		t2.start();
		t3.start();
	}
	
	public static void method1() { System.out.println("method 1");}
	public static void method2() { System.out.println("method 2");}
	public static void method3() { System.out.println("method 3");}
}
```

자바의 대표적인 비동기식 일처리로는 Multi-Thread의 동작이 있다. 각 메서드를 각각의 thread를 담아, start method를 통해 메서드를 수행하게 되면 비동기식 일처리가 일어나게 된다. 동기식 처리의 경우 순차적으로 일을 처리하지 않기 떄문에, 처리 순서를 보장할 수 없다.

![Untitled](%5BJava%5D%20Blo%2092ea1/Untitled%202.png)

![Untitled](%5BJava%5D%20Blo%2092ea1/Untitled%203.png)

# Blocking vs Non-Blocking

블로킹과 논블로킹은 다른 작업을 수행하는 주체를 어떻게 상대하는지가 중요하다

## Blocking

자신의 작업을 하다가 다른 작업 주체가 하는 작업의 시작부터 끝까지 기다렸다가 다시 자신의 작업을 시작

![Untitled](%5BJava%5D%20Blo%2092ea1/Untitled%204.png)

ex : Java에서 JDBC를 사용하여 DB에 쿼리를 날리고 결과를 받아오는 작업을 블록킹 작업이라고 할 수 있음

## Non-Blocking

다른 주체의 작업과 관계없이 자신의 작업을 계속함

![Untitled](%5BJava%5D%20Blo%2092ea1/Untitled%205.png)

다른 주체에게 작업을 요청하고 그 결과를 받을때까지 기다리지 않으며 자신의 작업을 한다면 논블로킹이라고 할 수 있음

# 동기/비동기와 블로킹/논블로킹의 조합

동기/비동기/블로킹/논블로킹 개념들은 조합을 해서 사용한다

## 동기 블로킹(Sync-Blocking)

![두개의 작업이 시작과 동시에 끝나는 시간이 일치 (sync ) + 한쪽에서 작업이 시작되면 다른쪽에서는 작업을 멈춤 (blocking)](%5BJava%5D%20Blo%2092ea1/Untitled%206.png)

두개의 작업이 시작과 동시에 끝나는 시간이 일치 (sync ) + 한쪽에서 작업이 시작되면 다른쪽에서는 작업을 멈춤 (blocking)

- Task 1이 Task2를 호출
- Task 2 수행 (이때, Task 1은 대기상태)
- Task 2가 끝남과 동시에 Task1이 제어권을 가져감
- Task 1은 Task2의 결과를 받음

## 비동기 논블로킹 (Async-Nonblocking)

![서로 시작과 끝 불일치 + 결과 기다림 x (async) + 각자 일처리 병행 가능 (Non blocking)](%5BJava%5D%20Blo%2092ea1/Untitled%207.png)

서로 시작과 끝 불일치 + 결과 기다림 x (async) + 각자 일처리 병행 가능 (Non blocking)

- Task 1이 Task 2 호출
- Task 1은 제어권을 유지한 채로 작업
- Task 2 작업 처리
- Task 2의 작업이 끝나고 결과 Call Back

## 동기 논블로킹 (Sync-Nonblocking)

![서로 시작과 끝시간 불일치 + 결과 기다림x (async) + 각자 일처리 병행 가능 (non-blocking)](%5BJava%5D%20Blo%2092ea1/Untitled%208.png)

서로 시작과 끝시간 불일치 + 결과 기다림x (async) + 각자 일처리 병행 가능 (non-blocking)

- Task 1이 Task 2 호출
- Task 1 제어권 유지
- Task 1은 작업 처리를 하며 Task 2의 완료 여부를 지속적으로 확인
- Task 2의 작업이 완료되면 Task1이 데이터 회신을 하고 나머지 작업 수행

## 비동기 블로킹 (Async-Blocking)

![Untitled](%5BJava%5D%20Blo%2092ea1/Untitled%209.png)

- Task 1 이 Task 2 호출
- Task 2가 제어권을 가져감
- Task 2 작업 처리 후 callback 반환
- Task 1 이 다시 제어권 가져감

다른 작업의 작업 마침여부를 기다리지는 않지만, 제어권이 작업중인쪽으로 넘어가기때문에 동기 블로킹과 비슷하게 동작함. 

<aside>
📌 비동기 블로킹은 효율적이지 않아 많이 사용되지 않으며, 결국 Task 1이 제어권을 잃기 때문에 비동기를 사용함에도 불구하고 비동기로 일처리를 할 수 없다.

</aside>

---

References

[https://siyoon210.tistory.com/147](https://siyoon210.tistory.com/147)

[https://webheck.tistory.com/entry/Java동기와-비동기-방식Asynchronous-processing-modelhttps://webheck.tistory.com/entry/Java동기와-비동기-방식Asynchronous-processing-model](https://webheck.tistory.com/entry/Java%EB%8F%99%EA%B8%B0%EC%99%80-%EB%B9%84%EB%8F%99%EA%B8%B0-%EB%B0%A9%EC%8B%9DAsynchronous-processing-model)

[https://deveric.tistory.com/99](https://deveric.tistory.com/99)

[https://camelsource.tistory.com/73](https://camelsource.tistory.com/73)