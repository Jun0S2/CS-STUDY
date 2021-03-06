# LinkedList - 혜준

## 정의

연결 리스트 (Linked List)로 각 노드가 데이터와 포인터를 가지고 한줄로 연결되어있는 방식의 자료 구조. 

1. 링크드리스트는 인덱스가 존재하지 않기 때문에 검색 및 수정 시 첫번째 노드부터 순차적으로 모든 노드를 탐색해야 한다 → 시간복잡도 : O(1)
2. **특정 위치(index)로** 삽입/삭제/탐색해야 하는 경우는 O(n) 이 걸린다. 따라서, 탐색을 자주해야 한다면 배열을 사용하고, 데이터의 추가/삭제가 많은 경우에 연결 리스트를 사용하는 것이 좋다.

![Untitled](LinkedList%208e337/Untitled.png)

연결리스트는 단일 연결리스트, 이중 연결리스트, 원형 연결리스트가 있다. 

## 단일 연결리스트 (Singly Linked List)

[단일 연결리스트 구현](LinkedList%208e337/%E1%84%83%E1%85%A1%E1%86%AB%E1%84%8B%E1%85%B5%E1%86%AF%20%E1%84%8B%E1%85%A7%E1%86%AB%20fcd47.md)

단일 연결리스트는 데이터의 요소를 선형적으로 연결한 것이다.

![단일 연결리스트: 하나의 노드에 한개의 포인터와 데이터값이 저장된다](LinkedList%208e337/Untitled.png)

단일 연결리스트: 하나의 노드에 한개의 포인터와 데이터값이 저장된다

1. 메모리와 디스크에 연속적으로 데이터를 할당해야하는 배열과는 다르게, 전체 구조를 재할당하거나 재구성하지 않고도 특정 지점에 요소를 추가하거나 제거할 수 있어서 유리하다.
2. 포인터로 다음 연결 리스트를 지정한다. 즉, 배열보다 더 많은 메모리를 사용하게 된다.
3. 단일 연결리스트는 특정 리스트값을 확인하기 위해서 리스트 안의 항목을 순차적으로 순회해야한다.

## 이중 연결리스트 (Doubly Linked List)

[이중 연결 리스트 구현](LinkedList%208e337/%E1%84%8B%E1%85%B5%E1%84%8C%E1%85%AE%E1%86%BC%20%E1%84%8B%E1%85%A7%E1%86%AB%E1%84%80%20a5cb3.md)

이중 연결리스트는 하나의 노드에 두개의 링크가 존재한다.

![이중 연결리스트 : 하나의 노드에 데이터값과, 이전과 다음 노드의 주소를 담은 포인터가 저장된다](LinkedList%208e337/Untitled%201.png)

이중 연결리스트 : 하나의 노드에 데이터값과, 이전과 다음 노드의 주소를 담은 포인터가 저장된다

1. 각 노드는 이전 노드의 참조 링크와, 다음 노드의 참조링크를 가지고 있다
2. 전체 노드를 순회해야 이전 노드를 찾을수 있는 단일 연결리스트와는 다르게, **이중 연결리스트는 이전 노드의 링크를 통해 O(1)의 시간 복잡도로 이전 노드를 찾을 수 있다**
3. 노드의 추가와 제거가 단일 연결리스트보다 많은 작업을 해야한다
4. 작업이 더 단순하고 잠재적으로 더 효율적이다

## 원형 연결리스트(Circular Linked List)

[원형 연결리스트 구현](LinkedList%208e337/%E1%84%8B%E1%85%AF%E1%86%AB%E1%84%92%E1%85%A7%E1%86%BC%20%E1%84%8B%E1%85%A7%E1%86%AB%2006fe8.md)

원형 연결리스트는 마지막 노드가 처음 노드를 가리키는 연결리스트이다

![원형 연결리스트: 마지막 노드가 처음 노드의 주소를 가리킨다](LinkedList%208e337/Untitled%202.png)

원형 연결리스트: 마지막 노드가 처음 노드의 주소를 가리킨다

단일 연결리스트와 달리, 이전 노드값을 탐색할 때 다시 순회할 필요 없이 연속적으로 탐색하여 노드를 찾아낼 수 있다.

## ArrayList VS LinkedList

ArrayList 는 데이터들이 순서대로 늘어선 배열의 형식을 취하고 있지만, LinkedList는 자료의 주소값으로 서로 연결된 형식을 갖기 때문에 둘의 장단점을 비교해 볼 수 있다.

### ArrayList

### LinkedList

1. 원하는 데이터에 무작위로 접근 가능
2. 리스트의 크기가 제한→ 리스트의 크기를 재조정은 많은 연산이 필요
3. 데이터의 추가/삭제시 임시 배열을 생성하고 복제 → 시간이 오래 걸림

1. 리스트의 크기에 영향 없이 데이터를 추가
2. 데이터를 추가하기 위해 새로운 노드를 생성하여 연결 →  추가와 삭제가 빠름
3. 무작위 접근이 불가능→ 순차 접근만 가능

---

# 기술 면접 예상 질문 리스트

문제 참고 사이트 : [https://career.guru99.com/top-17-linked-list-interview-questions/](https://career.guru99.com/top-17-linked-list-interview-questions/)

### 기본 개념

1. 링크드 리스트에 대해 설명해 보시오
2. 링크드 리스트의 종류에 대해 설명해보시오.
- 단일 링크드 리스트란?
- 이중 링크드 리스트란?
- 원형 링크드 리스트란?
1. 단일 링크드 리스트와 이중 링크드 리스트의 차이점에 대해 설명해보시오

### 더미 노드 - 잘 안나올 것 같은데 생소해서..

1. 링크드리스트의 더미 노드에 대해 설명해보시오 
    
    더미 노드는 사용하지 않아도 되는 노드이고 사용해도 되는 노드인데, dummy node를 사용한 경우 head 가 더미 노드를 가리킨다. 
    
    ![Untitled](LinkedList%208e337/Untitled%203.png)
    
    참고 사이트:
    [http://sjkitpro.blogspot.com/2018/07/linked-list-dummy.html](http://sjkitpro.blogspot.com/2018/07/linked-list-dummy.html) 
    

### 배열과 비교

1. 연결리스트를 사용했을 때 가장 큰 장점에 대해 기술해보시오
2. 링크드리스트와 배열의 차이점에 대해 설명해보시오

### 구현- 추가와 삭제하는 방법 숙지

1. 단일 링크드리스트의 시작노드에 신규 노드를 추가하는 방법에 대해 설명해 보시오
2. 단일 링크드 리스트의 처음 노드를 마지막 노드로 옮기는 방법에 대해 설명해보시오.