# Heap - 종대

## < 힙 >

- 완전 이진 트리의 일종으로 우선순위 큐를 위하여 만들어진 자료구조이다.
    1. **이진 트리** : 자식 노드가 두 개 이하인 트리
        
        ![Untitled](Heap%20-%20%E1%84%8C%E1%85%A9%E1%86%BC%20b362e/Untitled.png)
        
    
    1-1. 포화 이진 트리 : 리프 노드(단말 노드)를 제외한 모든 노드의 자식이 2개로 채워져 있는 트리
    
    1-2. 완전 이진 트리 : 이진 트리이지만 왼쪽부터 노드가 차곡차곡 순서대로 채워져 있는 트리
    
- 여러 개의 값들 중 최댓값이나 최솟값을 빠르게 찾아낼 수 있다.
    
    어떤 자료 구조에 값을 넣고 뺄 건데 어떤 경우가 되건 항상 자료구조 상태가 자동으로 **반정렬**된 상태여서 최대 최소값을 쉽게 이용하고 싶을 때 ( 반정렬된 상태? )
    

- **최대 힙**
    
    → 부모 노드의 키 값이 자식 노드의 키 값보다 크거나 같은 완전 이진 트리. 루트 노드에 **항상 최댓값**이 존재하게 된다.
    
- **최소 힙**
    
    → 부모 노드의 키 값이 자식 노드의 키 값보다 작거나 같은 완전 이진 트리. 루트 노드에 **항상 최솟값**이 존재하게 된다.
    

![Untitled](Heap%20-%20%E1%84%8C%E1%85%A9%E1%86%BC%20b362e/Untitled%201.png)

- **힙에서의 데이터 추가**

→ 부모 노드와 계속 비교해 나가면서 최댓/최솟값을 갱신해 나간다. 아무리 운이 나빠도 최대 트리의 높이만큼만 비교하면 데이터 추가 시에도 정렬 상태를 유지할 수 있다.

![Untitled](Heap%20-%20%E1%84%8C%E1%85%A9%E1%86%BC%20b362e/Untitled%202.png)

- **힙에서의 데이터 삭제**

→ 루트 노드 값을 삭제하고 마지막 인덱스에 있는 노드를 루트 노드로 올린 후 정렬과정을 거친다.

![Untitled](Heap%20-%20%E1%84%8C%E1%85%A9%E1%86%BC%20b362e/Untitled%203.png)

- 힙에서의 데이터 추가와 삭제는 반드시 마지막 인덱스 노드가 연관된다. 그리고 삽입과 삭제 후 부모 / 자식 노드와 비교하면서 정렬의 과정을 거치는데 이는 최대 log(n) 번 일어난다. (n은 노드의 총 개수, log(n)은 트리의 높이)

- **실제 구현**

→ 사실 눈에 보이는 구조가 트리이지 자바에는 이런 구조가 존재하지 않는다. 그래서 보통 1차원 배열로 구현한다. 어떻게 트리 모양을 1차원 배열에 넣을 수 있을까? 부모 노드와 자식 노드의 번호를 매길 때 발생하는 특정한 규칙을 이용한다.

### → **부모 노드와 자식 노드 관계**

`왼쪽 자식 index = (부모 index) * 2

오른쪽 자식 index = (부모 index) * 2 + 1

부모 index = (자식 index) / 2`

![Untitled](Heap%20-%20%E1%84%8C%E1%85%A9%E1%86%BC%20b362e/Untitled%204.png)

- 언제 사용할까?

→ 운영체제 메모리 관리 중 우선순위 스케줄링 방식

![Untitled](Heap%20-%20%E1%84%8C%E1%85%A9%E1%86%BC%20b362e/Untitled%205.png)

 → 알고리즘에서는 다익스트라 알고리즘에서 사용됨. 노드를 거치면서 계속 나랑 가장 가까운 노드를 탐색해 나가야 하기 때문

- **힙 구현 문제**  :  [https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV-Tj7ya3jYDFAXr&categoryId=AV-Tj7ya3jYDFAXr&categoryType=CODE&problemTitle=힙&orderBy=FIRST_REG_DATETIME&selectCodeLang=ALL&select-1=&pageSize=10&pageIndex=1](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV-Tj7ya3jYDFAXr&categoryId=AV-Tj7ya3jYDFAXr&categoryType=CODE&problemTitle=%ED%9E%99&orderBy=FIRST_REG_DATETIME&selectCodeLang=ALL&select-1=&pageSize=10&pageIndex=1)
- **힙 구현 참고 코드 :** [https://swexpertacademy.com/main/code/referenceCode/referenceCodeDetail.do?referenceId=test02&category=undefined](https://swexpertacademy.com/main/code/referenceCode/referenceCodeDetail.do?referenceId=test02&category=undefined)

- **자바에서의 힙 사용**

```java
// 기본적으로 큐와 사용 방법이 비슷함.
PriorityQueue<Integer> pq = new PriorityQueue<>();
// 자바는 기본적으로 모든 것이 오름차순, 따라서 힙도 최소 힙으로 생성된다.
pq.offer(8); // 우선순위 큐에 삽입
pq.offer(9); // 삽입
pq.offer(1); // 삽입
pq.poll(); // 우선순위 큐의 루트 노드를 뽑아옴. 항상 최솟값만 가져올 수 있음
// 삽입과 삭제후엔 내부적으로 정렬 과정이 실행되어서 힙 구조가 유지 됨.

PriorityQueue<Integer> pq2 = new PriorityQueue<>(Collections.reverseOrder());
// 생성자 인자에 Collections.reverseOrder()를 주면 최대 힙으로 생성 가능

// 보통 알고리즘 문제에서는 Integer 보다는 사용자 생성 객체를 넣는 경우가 많음
PriorityQueue<Student> pq3 = new PriorityQueue<>();
// 컴퓨터가 정수는 대소 비교를 어떻게 할 지 알고 있지만 사용자가 생성한 Student 객체는
// 어떻게 비교해야 하는지에 대한 정의가 없음. 그래서 반드시 그 정의를 만들어 줘야만 
// 힙 구조 생성 가능

class Student implements Comparable<Student>{
	int number;
	String name;
	@Override
	public int compareTo(Student other){
		if(this.number == other.number){

}

	}
}
// Comparable 인터페이스를 구현해서 비교에 대한 정의를 생성했음.
```