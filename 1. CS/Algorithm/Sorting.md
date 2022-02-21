# Sorting

## 정렬이란?
알고리즘 공부를 하며 배운 여러 자료구조, 알고리즘 등을 정리해보려고 합니다.   
정렬 알고리즘들은 기본적인 알고리즘이자 정말 많이 활용되는 알고리즘입니다.   
보통 언어의 기본 라이브러리 안에서 구현이 되어있어 호출로 간단히 사용할 수 있지만 직접 구현해야 하는 경우도 있고 무엇보다 어떤 식으로 돌아가는지를 알아야 다른 방법으로도 활용할 수 있습니다.   

### 버블정렬 (Bubble Sort)
정렬 중에서도 가장 쉽게 구현 가능한 버블정렬에 대해 알아보겠습니다.   
버블정렬의 아이디어는 간단합니다.    

1. N개의 데이터가 있을 때, N-1번의 비교를 통해 가장 뒤에 (방향에 따라 달라집니다.) 위치할 데이터를 알아내자.    
2. 이제 하나의 데이터는 자기 자리에 있으니 나머지 N-1개의 데이터를 가지고 비교를 해보자.   
3. 정렬이 완료될 때까지 계속 반복하자!   

그럼 한 번 비교가 이루어질때마다 1개씩 정렬되므로 N-1, N-2, N-3 ... 2,1 번 비교를 해야 합니다.   
전체적인 비교의 횟수는 (N*(N-1))/2가 되는데, 시간 복잡도를 말할 때는 보통 작은 차수나 계수를 지우고 표현하기 때문에 O(N^2)와 같이 나타냅니다.   

아래는 JAVA로 구현한 간단한 버블정렬 코드와 테스트입니다!   
이것저것 바꿔보고 디버깅하면서 흐름이 이해되시길 바랍니다.   

<details markdown="1">
<summary>코드 접기/펼치기</summary>

```Java
import java.util.Arrays;
import java.util.Random;

public class 01_sort_01_bubble {
	static int size = 100;
	static int bound = 1000;
	// 데이터의 갯수와 범위 설정

	public static void main(String[] args) {
		int[] data = new int[size];
		Random random = new Random();
		int count = 0;

		for (int i = 0; i < size; i++) {
			data[i] = random.nextInt(bound);
		}
		// 랜덤 값 넣어주기

		System.out.println(Arrays.toString(data));
		// 랜덤하게 들어간 데이터 확인

		/////////////////////// 버블정렬 구현////////////////////////////
		for (int find = size - 1; find >= 0; find--) {
			for (int now = 0; now < find; now++) {
				int next = now + 1;
				if (data[now] > data[next]) {
					int save = data[now];
					data[now] = data[next];
					data[next] = save;
				}
				count++;
			}
		}
		//////////////////////////////////////////////////////

		System.out.println(Arrays.toString(data));
		System.out.println("비교횟수 : " + count);
		// 정렬 후 데이터와 비교횟수 확인

		int[][] data2 = { { 1, 1 }, { 3, 1 }, { 5, 1 }, { 7, 1 }, { 9, 1 }, { 1, 2 }, { 2, 2 }, { 4, 2 }, { 1, 3 },
				{ 7, 2 }, { 9, 3 }, { 3, 3 }, { 4, 3 }, { 8, 3 }, { 6, 3 } };
		for (int find = 14; find >= 0; find--) {
			for (int now = 0; now < find; now++) {
				int next = now + 1;
				if (data2[now][0] > data2[next][0]) {
					int[] save = data2[now].clone();
					data2[now] = data2[next].clone();
					data2[next] = save.clone();
				}
			}
		}

		for (int i = 0; i < 15; i++) {
			System.out.printf("정렬된 수 : %d, stable: %d\n", data2[i][0], data2[i][1]);
		}
		//stable 정렬임!
	}
}
```
</details>


### 선택정렬 (Selection Sort)
선택 정렬의 아이디어도 간단합니다.

1. 첫번째 데이터부터 탐색해 가장 작은 수를 찾아 첫 번째 위치로 옮긴다. (오름, 내림차순에 따라 다릅니다.)   
2. 이제 첫번째 위치는 정렬되었으니, 두 번째 데이터부터 탐색한다.   
3. 정렬이 완료될때까지 계속 반복한다!   


선택 정렬도 한 번 비교가 이루어질 때마다 데이터가 1개씩 정렬되므로 N-1, N-2, N-3 ... 2, 1 번 비교를 해야 합니다.   
전체적인 비교의 횟수는 (N*(N-1))/2가 되고, 시간 복잡도는 O(N^2)와 같이 나타냅니다.   
다만, 매 번 데이터의 교체가 필요한 버블정렬과 달리 선택 정렬은 위치를 찾은 뒤 마지막에 한 번만 교체하면 되니 버블 정렬보다는 빠르게 정렬이 이루어집니다.   
대신 선택정렬의 경우는 stable하지 않은 불안정 정렬인데, 이 내용은 차후에 다루도록 하겠습니다.   

아래에는 JAVA로 구현한 간단한 선택정렬 코드와 테스트입니다!   
이것저것 바꿔보고 디버깅하면서 흐름이 이해되시길 바랍니다.   

<details markdown="1">
<summary>코드 접기/펼치기</summary>

```Java
import java.util.Arrays;
import java.util.Random;

public class sort_02_selection {
	static int size = 10;
	static int bound = 1000;
	// 데이터의 갯수와 범위 설정

	public static void main(String[] args) {
		int[] data = new int[size];
		Random random = new Random();
		int count = 0;

		for (int i = 0; i < size; i++) {
			data[i] = random.nextInt(bound);
		}
		// 랜덤 값 넣어주기

		System.out.println(Arrays.toString(data));
		// 랜덤하게 들어간 데이터 확인

		/////////////////////// 선택정렬 구현////////////////////////////
		for (int find = 0; find < size; find++) {
			int minIdx = find;
			for (int now = find; now < size; now++) {
				if(data[now] < data[minIdx]) {
					minIdx = now;
				}
				count++;
			}
			int save = data[find];
			data[find] = data[minIdx];
			data[minIdx] = save;
		}
		//////////////////////////////////////////////////////

		System.out.println(Arrays.toString(data));
		System.out.println("비교횟수 : " + count);
		// 정렬 후 데이터와 비교횟수 확인

		int[][] data2 = { { 1, 1 }, { 3, 1 }, { 5, 1 }, { 7, 1 }, { 9, 1 }, { 1, 2 }, { 2, 2 }, { 4, 2 }, { 1, 3 },
				{ 7, 2 }, { 9, 3 }, { 3, 3 }, { 4, 3 }, { 8, 3 }, { 6, 3 } };
		
		for (int find = 0; find < 15; find++) {
			int minIdx = find;
			for (int now = find; now < 15; now++) {
				if(data2[now][0] < data2[minIdx][0]) {
					minIdx = now;
				}
				count++;
			}
			int[] save = data2[find].clone();
			data2[find] = data2[minIdx].clone();
			data2[minIdx] = save.clone();
		}

		for (int i = 0; i < 15; i++) {
			System.out.printf("정렬된 수 : %d, stable: %d\n", data2[i][0], data2[i][1]);
		}
		// stable 정렬이 아님!
	}
}
```

</details>


### 삽입정렬 (Bubble Sort)
삽입정렬은 간단히 말해서 우리가 실생활에서 쓰는 정렬법입니다.   
도둑잡기나 원카드 같은 카드게임을 할 때, 카드를 뽑아서 자기 자리에 끼우면서 정렬하는 그 방식을 생각하시면 됩니다.   

1. 정렬되지 않은 데이터 중에 하나를 고른다.   
2. 선택한 데이터를 정렬된 데이터와 비교해서 들어갈 위치를 찾는다.    
3. 정렬이 완료될 때까지 계속 반복한다!   


삽입정렬은 앞서 배웠던 버블정렬, 선택정렬보다 조금 속도가 빠르다고 합니다.   
버블정렬, 선택정렬은 정렬되지 않은 모든 데이터와 비교를 해서 정렬 횟수가 고정되어있는 반면, 삽입 정렬은 정렬된 데이터와 비교를 하기 때문에 자신의 위치를 찾을 때까지만 비교합니다.   
물론 최악의 경우(역순으로 정렬된 상태)에는 버블, 선택정렬과 똑같은 수를 비교합니다.   
또한 데이터가 들어갈 위치를 찾는 방법, 데이터들을 shift 하는 방법에 따라 효율이 조금씩 달라진다고 합니다.   

<details markdown="1">
<summary>코드 접기/펼치기</summary>

```Java
import java.util.Arrays;
import java.util.Random;

public class sort_03_insertion {
	static int size = 10;
	static int bound = 1000;
	// 데이터의 갯수와 범위 설정

	public static void main(String[] args) {
		int[] data = new int[size];
		Random random = new Random();
		int count = 0;

		for (int i = 0; i < size; i++) {
			data[i] = random.nextInt(bound);
		}
		// 랜덤 값 넣어주기

		System.out.println(Arrays.toString(data));
		// 랜덤하게 들어간 데이터 확인

		/////////////////////// 삽입정렬 구현////////////////////////////
		for (int s = 0; s < size; s++) {
			int now = s;
			while (now > 0) {
				if(data[now] < data[now-1]) {
					int save = data[now];
					data[now] = data[now-1];
					data[now-1] = save;
				}else {
					break;
				}
				now--;
				count++;
			}
		}
		//////////////////////////////////////////////////////

		System.out.println(Arrays.toString(data));
		System.out.println("비교횟수 : " + count);
		// 정렬 후 데이터와 비교횟수 확인

		int[][] data2 = { { 1, 1 }, { 3, 1 }, { 5, 1 }, { 7, 1 }, { 9, 1 }, { 1, 2 }, { 2, 2 }, { 4, 2 }, { 1, 3 },
				{ 7, 2 }, { 9, 3 }, { 3, 3 }, { 4, 3 }, { 8, 3 }, { 6, 3 } };
		
		for (int s = 0; s < 15; s++) {
			int now = s;
			while (now > 0) {
				if(data2[now][0] < data2[now-1][0]) {
					int[] save = data2[now].clone();
					data2[now] = data2[now-1].clone();;
					data2[now-1] = save;
				}else {
					break;
				}
				now--;
				count++;
			}
		}

		for (int i = 0; i < 15; i++) {
			System.out.printf("정렬된 수 : %d, stable: %d\n", data2[i][0], data2[i][1]);
		}
		// stable 정렬이 아님!
	}
}
```

</details>

### 병합정렬 (Merge Sort)
<details markdown="1">
<summary>코드 접기/펼치기</summary>

```Java
```

</details>

### 퀵정렬 (Quick Sort)
<details markdown="1">
<summary>코드 접기/펼치기</summary>

```Java
```

</details>

### 기수정렬 (Radix Sort)
<details markdown="1">
<summary>코드 접기/펼치기</summary>

```Java
```

</details>

### 카운팅정렬 (Counting Sort)
<details markdown="1">
<summary>코드 접기/펼치기</summary>

```Java
```

</details>