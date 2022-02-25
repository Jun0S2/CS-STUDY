# 삽입정렬, 병합정렬 - 호연

## cf. 안정 정렬 vs 불안정 정렬

### 안정 정렬(Stable Sort)

중복된 값을 입력 순서와 동일하게 정렬되는 알고리즘

ex) 삽입정렬, 병합정렬, 버블정렬

### 불안정 정렬(Unstable Sort)

안정 정렬과 반대로 중복된 값이 입력 순서와 동일하지 않게 정렬되는 알고리즘

ex) 퀵 정렬, 선택정렬, 계수정렬

# 삽입정렬(Insertion Sort)

선택 정렬에 비해 실행 시간 측면에서 더 효율적인 알고리즘

특히, 필요할 때만 위치를 바꾸므로 ***'데이터가 거의 정렬 되어있을 때'*** 훨씬 효율적

특정한 데이터를 적절한 위치에 '삽입'한다는 의미에서 **삽입정렬**이다.

특정한 데이터가 적절한 위치에 들어가기 이전에, 그 앞까지의 데이터는 이미 정렬되었다고 가정

정렬되어 있는 데이터 리스트에서 적절한 위치를 찾은 뒤에, 그 위치에 삽입된다는 것이 특징이다.

## 예제

**[Step 0]** 첫 번째 데이터 '7'은 그 자체로 정렬이 되어 있다고 판단하고, 두 번째 데이터인 '5'가 어떤 위치로 들어갈지 판단한다. '7'의 왼쪽으로 들어가거나 오른쪽으로 들어가는 두 경우만 존재

![Untitled](%E1%84%89%E1%85%A1%E1%86%B8%E1%84%8B%E1%85%B5%E1%86%B8%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%20af2fc/Untitled.png)

**[Step 1]** 이어서 '9'가 어떤 위치로 들어갈지 판단

![Untitled](%E1%84%89%E1%85%A1%E1%86%B8%E1%84%8B%E1%85%B5%E1%86%B8%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%20af2fc/Untitled%201.png)

**[Step 2]** 이어서 '0'이 어떤 위치로 들어갈지 판단

![Untitled](%E1%84%89%E1%85%A1%E1%86%B8%E1%84%8B%E1%85%B5%E1%86%B8%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%20af2fc/Untitled%202.png)

... 같은 방식으로 마지막 index까지 반복하면 완료

![Untitled](%E1%84%89%E1%85%A1%E1%86%B8%E1%84%8B%E1%85%B5%E1%86%B8%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%20af2fc/Untitled%203.png)

```java
/* 삽입정렬 */
int[] array = {7, 5, 9, 0, 3, 1, 6, 2, 4, 8};

for(int i = 1; i < array.length; i++){
		for(int j = i; j > 0; j--){        
				if(array[j] < array[j - 1]){   // 한 칸씩 왼쪽으로 이동
						int temp = array[j];
						array[j] = array[j - 1];
						array[j - 1] = temp;
				}else{  // 자기보다 작은 데이터를 만나면 그 위치에서 멈춤
						break;
				}
		}
}
```

### 평균과 최악의 시간복잡도 : O(N^2)

**But,** 삽입정렬은 현재 리스트의 데이터가 ***거의 정렬되어 있는 상태라면***  매우 빠르게 동작한다.

최선의 경우(Best case) O(N)의 시간 복잡도를 가진다.

보통은 삽입정렬이 비효율적이나, ***정렬이 거의 되어 있는 상황*** 에서는 퀵 정렬 알고리즘보다 더 강력하다.(탐색을 제외한 오버헤드가 매우 적기 때문)

# 병합정렬(Merge Sort)

분할 정복 알고리즘의 한 종류

**분할 정복(Divide and conquer)**이란?

- 문제를 작은 2개의 문제로 분리하고 각각을 해결한 다음, 결과를 모아서 원래의 문제를 해결하는 전략

**과정 설명**

1) 리스트의 길이가 0 또는 1이면 이미 정렬된 것으로 본다. 그렇지 않은 경우에는

2) **분할(Divide)** :  정렬되지 않은 배열을 절반으로 잘라 2개의 부분 배열로 분할한다.

3) **정복(Conquer)** : 각 부분 배열을 재귀적으로 합병 정렬을 이용해 정렬한다.

4) **결합(Combine)** : 정렬된 부분 배열들을 하나의 정렬된 배열에 합병한다.

![Untitled](%E1%84%89%E1%85%A1%E1%86%B8%E1%84%8B%E1%85%B5%E1%86%B8%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%20af2fc/Untitled%204.png)

***퀵소트와의 차이점***

퀵정렬 : 우선 피벗을 통해 정렬(partition) → 영역을 쪼갬(quickSort)

합병정렬 : 영역을 쪼갤 수 있을 만큼 쪼갬(mergeSort) → 정렬(merge)

## 예제

- 배열에 [21, 10, 12, 20, 25, 13, 15, 22]이 저장되어 있다고 가정하고 자료를 오름차순으로 정렬해 보자.
- *2개의 정렬된 리스트를 합병(merge)하는 과정*
    
    1) 2개의 리스트의 값들을 처음부터 **하나씩 비교하여** 두 개의 리스트의 값 중에서 더 작은 값을 새로운 리스트(sorted)로 옮긴다.
    
    2) 둘 중에서 하나가 끝날 때까지 이 과정을 되풀이한다.
    
    3) 만약 둘 중에서 하나의 리스트가 먼저 끝나게 되면 나머지 리스트의 값들을 전부 새로운 리스트(sorted)로 복사한다.
    
    4) 새로운 리스트(sorted)를 원래의 리스트(list)로 옮긴다.
    

```java
public class MergeSortTest {
		public static void main(String[] args) {
				int[] array = {21, 10, 12, 20, 25, 13, 15, 22};
			 
				// 합병 정렬 수행(left: 배열의 시작 = 0, right: 배열의 끝 = 7)
		    mergeSort(array, 0, array.length - 1);
		 
		    // 정렬 결과 출력
		    for (int v : array) {
		        System.out.print(v + " ");
		    }
		}
		 
		// 합병 정렬
		public static void mergeSort(int[] array, int left, int right) {
		    if (left < right) {
		        int mid = (left + right) / 2;		// 중간 위치 계산
		 
		        // Divide & Conquer (배열을 균등 분할 & 배열 정렬)
		        mergeSort(array, left, mid);		// 앞쪽 배열 정렬
		        mergeSort(array, mid + 1, right);	// 뒤쪽 배열 정렬
		        
		        // Combine
		        merge(array, left, mid, right);		// 정렬된 2개의 부분 배열을 합병
		    }
		}
		
		
		// i: 정렬된 왼쪽 리스트에 대한 인덱스
		// j: 정렬된 오른쪽 리스트에 대한 인덱스
		// k: 정렬될 리스트에 대한 인덱스
		/* 2개의 인접한 배열 array[left...mid]와 array[mid+1...right]의 합병 과정 */
		/* (실제로 숫자들이 정렬되는 과정) */
		public static void merge(int[] array, int left, int mid, int right) {
		    int[] L = Arrays.copyOfRange(array, left, mid + 1);
		    int[] R = Arrays.copyOfRange(array, mid + 1, right + 1);
		 
		    int i = 0, j = 0, k = left;
		    int ll = L.length, rl = R.length;
		 
		    // 분할 정렬된 array의 합병
		    while (i < ll && j < rl) {
		        if (L[i] <= R[j]) {
		            array[k] = L[i++];
		        } else {
		            array[k] = R[j++];
		        }
		        k++;
		    }
		 
		    // 남아있는 값 일괄 복사
		    while (i < ll) {
		        array[k++] = L[i++];
		    }
		 
		    // 남아있는 값 일괄 복사
		    while (j < rl) {
		        array[k++] = R[j++];
		    }
		}
}
```

### 시간복잡도 : O(NlogN)

이미 합병의 대상이 되는 두 영역이 각 영역에 대해서 정렬이 되어있기 때문에 단순히 두 배열을 **순차적으로 비교하**면서 정렬할 수가 있다.

***합병정렬은 순차적인 비교로 정렬을 진행하므로, LinkedList의 정렬이 필요할 때 사용하면 효율적이다.***

**LinkedList를 퀵정렬을 사용해 정렬하면?**

- 성능이 좋지 않음. 퀵정렬은, 순차 접근이 아닌 임의 접근이기 때문

**LinkedList는 삽입, 삭제 연산에서 유용**하지만 **접근 연산에서는 비효율적**임

- 따라서 임의로 접근하는 퀵소트를 활용하면 오버헤드 발생이 증가하게 됨

cf. 배열은 인덱스를 이용해서 접근이 가능하지만, LinkedList는 Head부터 탐색해야 함

접근 : 배열[O(1)] vs LinkedList[O(n)]