# [Java] GC

## 메모리 누수 (Memory Leak) 방지

자바는 OS의 메모리 영역에 직접적으로 접근하지 않고, JVM이라는 가상 머신을 이용해 간접적으로 접근한다. 프로그램 실행시 JVM 옵션을 주어서 OS에서 요청한 사이즈 만큼의 메모리를 할당 받아서 실행하게 되고, 할당받은 이상의 메모리를 사용하면 에러가 나면서 자동으로 프로그램이 종료된다. 따라서, 현재 프로세스에서 메모리 누수가 발생하더라도 현재 실행중인것만 죽고 다른것에는 영향을 주지 않는다. 이렇게 자바는 가상 머신을 사용함으로써 OS 레벨에서 메모리 누수를 막는데, **자바의 메모리 누수 현상을 방지하는 또 다른 방식이 가비지 컬렉션이다.**

## 가비지 컬렉션

가비지 컬렉션은 동적 할당된 메모리 영역(heap) 중에서 더이상 사용하지 않는 영역을 탐지하여 자동으로 해지하는 기법이다. Java에서는 개발자가 프로그램 코드로 메모리를 명시적으로 해제하지 않기 때문에 가비지 컬렉터가 더이상 필요없는 객체를 찾아 지우는 작업을 한다.

## 동작 원리

> 메모리 할당 → heap 내의 객체 중 가비지를 찾음 → 힙의 메모리 회수
> 

JVM의 메모리는 크게 4가지 영역으로 나뉜다 : 클래스 영역, 자바 스택, 힙, 네이티브 메소드 스택 
가비지 컬렉터는 이중에서 heap 메모리를 다룬다.

## 전제 조건

가비지 컬렉터는 두가지 전제 조건아래에 만들어졌다

**Weak Generational Hypothesis**

1. 대부분의 객체는 금세 접근 불가능 상태(unreachable)가 된다
2. 오래된 객체에서 젊은 객체로의 참조는 아주 적게 존재한다

즉, 객체는 대부분 일회성이며 메모리에 오랫동안 남아있는 경우는 드물다는 것이다. 따라서, 객체의 생존 기간에 따라 물리적인 Heap 영역을 나누게 되었는데 Young 과 Old 두가지 영역으로 나누었다. 이를 HotSpot Heap 구조라고 한다.
** 초기에는 Perm 영역이 존재했는데 Java8부터 제거되었다

![이미지 출처 : Stack Overflow](%5BJava%5D%20GC%209933a/Untitled.png)

이미지 출처 : Stack Overflow

- Young Generation (Young 영역)
- 새롭게 생성된 객체가 할당되는 영역
- 대부분의 객체가 금방 unreachable 상태가 되기 때문에 많은 객체가 young 영역에서 생성되었다 사라진다.
- Young 영역에 대한 가비지 컬랙션을 Minor GC라고 부른다
- Old Generation (Old 영역)
- Young 영역에서 reachable 상태를 유지하여 살아남은 객체가 복사되는 영역
- 복사되는 과정에서 대부분 young 영역보다 크게 할당되며, 크기가 큰만큼 가비지는 적게 발생
- Old 영역에 대한 가비지 컬랙션을 Major GC 또는 Full GC라고 부른다

## 동작 방식

### Minor GC

Young 영역은 1개의 Eden 영역과 2개의 Survivor 영역으로 나뉜다

- Eden 영역: 새로 생성된 객체가 할당되는 영역
- Survivor영역: 최소 1번 이상의 GC가 살아남은 객체가 존재하는 영역

새로 생성된 대부분의 객체(instance) 는 Eden 영역에 위치한다. Eden 영역에서 GC가 한 번 발생한 후 살아남은 객체는 Survivor 영역 중 하나로 이동된다. 이 과정을 반복하다가 계속해서 살아남아있는 객체는 일정시간 참조되고 있다는 뜻이므로 Old 영역으로 이동시킨다.

### Major GC

객체들이 계속 Young 영역에서 Old 영역으로 들어와서 메모리가 부족해지면, Old 영역에 있는 모든 객체들을 검사하여 참조되지 않은 객체들을 한꺼번에 삭제한다. 시간이 오래 걸리고 실행중 프로세스가 정지하는데 이를 'Stop the world- 라고 함. Major GC가 발생하면 GC를 실행하는 스레드를 제외한 나머지 스레드는 모든 작업을 중단시켰다가 GC가 완료된 이후에 다시 시작한다.

Major GC는 Young 영역보다 메모리 공간이 크기 때문에 가비지 컬렉팅을 하는 시간이 minor gc보다 10배 이상이 걸린다.

### GC가 소멸 대상을 선정하는 원리

참조되고 있지 않은 객체(instance)를 가비지라고 하며 객체가 가비지인지 판단하기 위해서 reachability 라는 개념을 사용한다.
어떤 영역에 할당된 객체가 유효한 참조가 있으면 reachability, 없으면 unreachability로 판단한다. 하나의 객체는 다른 객체를 참조하고 다른 객체는 또 다른 객체를 참조할 수 있기 때문에 참조 사슬이 형성되는데 이 참조 사슬 중 최초에 참조한 것을 Root Set이라고 한다.

![Untitled](%5BJava%5D%20GC%209933a/Untitled%201.png)

Root Set으로 부터 시작한 참조 사슬에 속한 객체들은 reachable object이고, 그렇지 않으면 가비지라고 판단되어 가비지 컬렉팅의 대상이 된다.

## 가비지 컬렉팅의 실행 시기

JVM이 언제 GC를 실행시키는지 보장할 수 없다. 하지만, GC를 요청시킬 수 있다.

```java
System.gc(); //Java System클래스의 gc 메서드
Runtime.getRuntime().gc();//Runtime class의 gc 메서드
```

[GC 내용 요약](%5BJava%5D%20GC%209933a/GC%20%E1%84%82%E1%85%A2%E1%84%8B%E1%85%AD%E1%86%BC%20%E1%84%8B%20d786e.csv)

참조:

[https://ko.myservername.com/what-is-garbage-collection-java](https://ko.myservername.com/what-is-garbage-collection-java)

[https://asfirstalways.tistory.com/159](https://asfirstalways.tistory.com/159)

[https://yaboong.github.io/java/2018/06/09/java-garbage-collection/](https://yaboong.github.io/java/2018/06/09/java-garbage-collection/)

[https://mangkyu.tistory.com/118](https://mangkyu.tistory.com/118)