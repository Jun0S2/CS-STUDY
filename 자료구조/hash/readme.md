# Hash

### [기본 동작](https://jtoday.tistory.com/73)

<br>

## 해시 정의

- ### 임의의 크기를 가진 데이터를 고정된 크기의 데이터로 변화 시켜 저장하는 것,
- ### 키에 대한 해시값을 구하는 과정을 hashing(해싱)이라고 하며 이때 사용하는 함수를 해시함수라 한다.
<br>

## 해시 함수

- ### 키를 고정된 길이의 hash로 변경해주는 역할을 한다. -> 이 과정을 hashing 이라 함
<br>

## 해시값 만드는 방법

### 해시테이블의 크기 = M 원소는 k라 가정

![image](https://user-images.githubusercontent.com/71022555/144976816-77484761-ccea-48c7-8931-6644d252848e.png)

### 1. 나눗셈법

원소를 해시테이블의 크기로 나누어 나머지 값을 테이블의 주소로 사용하는 방법 -> 테이블의 크기보다 원소의 개수가 많으면 충돌이 일어난다. -> h(k) = k%m
<br>

### 2. 곰셈법

0<A<1 인 A 에 대해서 다음과 같이 구할 수 있다.
h(k)=N(k*A*mod(%) 1) \* m -> m은 얼마든 상관없지만 보통 2의 제곱수로 정한다.
kAmod1 kA 의 소수점 이하 부분을 말하며 이를 NN 에 곱하므로 0부터 NN 사이의 값이 된다. 이 방법의 장점은 NN 이 어떤 값이더라도 잘 동작한다는 것이며 A 를 잘 잡는 것이 중요하다.
<br>

### 3. Universal Hasing

같은 자리에 여러 개의 키가 해시되는 것을 막기 위하여 실제 저장되는 키들과 독립적인 해시 함수를 무작위로 선택하는 것 -> 실행 중 계속 무작위가 아니라 프로그램이 돌 때마다 그 때마다 무작위로 선택해서 진행하므로 검색과 삭제하는데 상관이 없다. -> Math.Random() 느낌
[추가설명](https://coding-wonderland.tistory.com/14)
<br>

---

## 해시 테이블

### 개념

### 해시함수를 사용하여 변환한 값을 색인으로 삼아 키와 데이터를 저장하는 자료구조를 만한다. 기본연산으로는 탐색, 삽입, 삭제가 있다.

<br>

### 적재율

- ### 적재율이란 해시 테이블의 크기 대비, 키의 개수를 말한다. 즉, 키의 개수를 K, 해시 테이블의 크기를 N 이라고 했을 때 적재율은 K/N 이다.
- ### Direct Address Table은 키 값을 인덱스로 사용하는 구조이기 때문에 적재율이 1 이하이며 적재율이 1 초과인 해시 테이블의 경우는 반드시 충돌이 발생하게 된다. ex -> 배열 8개에 9개 넣을 수 없다.
<br>

### 성능

![image](https://user-images.githubusercontent.com/71022555/144977478-df2c37b2-8a33-4ae1-99e3-2d40f952d2ec.png)
<br>

---

### 해시 충돌 해결

![image](https://user-images.githubusercontent.com/71022555/144977571-ab6ffe9e-ba68-409c-ad08-b6e1d949e4e4.png)
<br>

## 1. Chainning

![image](https://user-images.githubusercontent.com/71022555/144977258-8b887780-6421-493b-ace4-4fab22033bc4.png)

### 평균 시간복잡도 : O(1) -> 해시값 자체를 index로 사용하기 때문에

<br>

[추가설명](https://baeharam.github.io/posts/data-structure/hash-table/)
