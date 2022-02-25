# 기수정렬, 계수정렬 - 혜준

# 기수 정렬 (Radix Sort)

<aside>
📌 자릿수를 비교하여 정렬하는 알고리즘
최악의 시간복잡도 : O(n) → 많은 양의 저장 공간을 차지함

</aside>

### 정의

기수 정렬 (Radix Sort) 는 **자릿수를 비교하여 정렬**하는 알고리즘으로, 각 요소를 비교하지 않고 정렬하는 알고리즘이다. 각 **자리수에 해당하는 버킷을 준비하고 1의 자리부터 제일 큰 수의 자리수까지 넣었다 뺐다를 반복**한다.

1. 시간복잡도
    - 최악 & 최고 시간복잡도 : $O(n)$ →매우빠른편
2. 메모리
    - 많은 양의 저장 공간을 차지한다

### 메커니즘

1. 배열의 요소가 숫자일 경우, **0~9까지의 자리수 만큼의 버킷을 준비**한다
2. 최초에는 1의자리수를 비교하고 1의자리수와 동일한 번호의 버킷에 요소를 넣는다
3. 다음 자리수들을 2번과정을 반복하여 버킷을 채운다
4. 배열 요소가 갖는 **최대 자리수만큼 버킷에 넣었다 빼면 최종 정렬된 배열 리스트**를 얻을 수 있다

[50,20,2,3,4 557]→ 

50 20 02 03 04 557

0 0 00000000000000000000000000000000000000000000000000000000000000

0~9 [0000000000]

002 003 004  020 050,557

![Bill Shantang 블로그](%E1%84%80%E1%85%B5%E1%84%89%E1%85%AE%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%E1%85%A7%E1%86%AF%208fd92/radixSort.gif)

Bill Shantang 블로그

### 구현

```java
//출처 : journee912 github
import java.util.Arrays;

public class RadixSort {
	// 최대값: 최대값 자리수만큼 돌아야 하기 때문에 필요
	static int getMax(int[] given) {
		int max = given[0];
		for(int i=1; i<data.length; i++) {max = given[i]>max? given[i]: max;}	}
		return max;
	}
	// exp 변수의 수에 따라 숫자를 정렬
	static void countSort(int[] data, int exp) {
		int[] output = new int[data.length];
		int[] count = new int[10];
		
		// count 값 count배열에 저장
		for(int i=0; i<data.length; i++) {
			count[(data[i]/exp)%10]++;
		}
		// count 값이 포함시켜 count배열에 저장
		for(int i=1; i<10; i++) {
			count[i] += count[i-1];
		}
		// output배열 빌드
		for(int i=data.length-1; i>=0; i--) {
			output[count[(data[i]/exp)%10]-1] = data[i];
			count[(data[i]/exp)%10]--;
		}
		// output 배열에 저장된 값을 data 배열에 저장
		for(int i=0; i<data.length; i++) {
			data[i] = output[i];
		}
	}

	static void radixsort(int[] data) {
		// 최대값 찾기
		int m = findMax(data);
		for(int exp=1; m/exp>0; exp*=10) {
			countSort(data, exp);
		}
	}

	public static void main(String[] args) {
		int [] data = {4, 54, 2, 8, 63, 7, 55, 56};
		// 기수 정렬 전
		System.out.println("# 기수 정렬 전");
		for(int i=0; i<data.length; i++) {
			System.out.print(data[i]+" ");
		}
		System.out.println();
		
		radixsort(data);
		// 기수 정렬 후
		System.out.println("# 기수 정렬 후");
		for(int i=0; i<data.length; i++) {
			System.out.print(data[i]+" ");
		}
	}

}
```

# 계수 정렬 (Counting Sort)

<aside>
📌 각 숫자의 카운팅 배열을 활용하여 정렬하는 알고리즘
범위조건이 있는 경우에 한해서 굉장히 빠른 알고리즘

</aside>

### 정의

계수 정렬 (Counting Sort)는 기수 정렬(Radix Sort) 와 마찬가지로 **각 요소를 비교하지 않고 정렬**하는 알고리즘이다. 원소간 직접 비교하지 않고 **각 원소가 몇개 등장하는지의 개수를 세서 정렬하는 방식이다.**

1. 시간 복잡도
    - $O(n+k)$로 퀵이나 병합정렬보다 빠름
    - $k< n$인 경우:  $O(n)$의 속도를 가짐
    - $k$가 매우 클 경우:  $O(∞)$
2. 메모리
    - 다른 정렬에 비해 많은 메모리가 사용됨

### 메커니즘

1. 카운팅 배열 초기화
2. 카운팅 배열에 각 원소의 사용횟수 추가
3. 카운팅 배열의 원소만큼 인덱스를 출력한다

![ Given Array 가 [2,3,8,7,1,2,2,2,7,3,9,8,2,1,4,2,4,6,9,2]일 떄 계수 정렬 - bill.shantang 블로그](%E1%84%80%E1%85%B5%E1%84%89%E1%85%AE%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%E1%85%A7%E1%86%AF%208fd92/countingSort.gif)

 Given Array 가 [2,3,8,7,1,2,2,2,7,3,9,8,2,1,4,2,4,6,9,2]일 떄 계수 정렬 - bill.shantang 블로그

### 구현

Given Array :  [5,3,8,1,5]일 때, 계수 정렬 메커니즘:

1. 카운팅 배열 초기화 : [0,0,0,0,0,0,0,0,0] //0~8 
2. 카운팅 배열에 각 원소의 사용 횟수 추가: [0,1,0,1,0,2,0,0,1]
3. 카운팅 배열만큼 각 인덱스를 출력한다  : 1 3 5 5 8

```java
static int array[] = {5,3,8,1,5};
static int size = 8;
/*count array index : 출력할 값
 *count array elements: 출력해야 하는 횟수 */
	public static CountingSort(){
		//counting array 초기화
		int[] count = new int[size+1]; //0~size 까지

		//현재 배열-> 카운트 (원소의 비교없이 sorting됨)
		for(int i =0; i< array.length; i++){ count[array[i]]++;	} 

		//출력
		for(int i =0; i< count.length ; i++){
			if(count [i]==0) continue; //0일 경우 출력x
			else{
					for(int j =0; j < count[i] ; j++){  //카운트배열의 원소 == 출력횟수
						System.out.print(i);   }          //인덱스==값 출력			
				} //end of else
		} //end of print

}//end of method
```

참고 사이트 : 

[8 Classical Sorting Algorithms](https://medium.com/@bill.shantang/8-classical-sorting-algorithms-d048eec3fdab)

[11. 계수 정렬(Counting Sort)](https://m.blog.naver.com/ndb796/221228361368)

[[Algorithm] Radix Sort(기수 정렬) : 자릿수를 비교하여 정렬하는 알고리즘](https://joycestudios.tistory.com/61?category=859593)