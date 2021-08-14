## **Baekjoon > 재귀 > 에너지 모으기**

</br>

[연습 문제 링크](https://www.acmicpc.net/problem/16198)

</br>

:books: 내가 사용한 프로그래밍 언어 : Java

</br>

## 문제 요약

N개의 에너지 구슬을 이용해서 에너지를 모으려고 한다.  
i번째 에너지 구슬의 에너지는 W[i]이며, 에너지를 모으는 방법은 다음과 같고, 반복해서 사용할 수 있다.

1. X번째 에너지 구슬 하나를 고른다.  
   첫번째 구슬과 마지막 구슬은 고를 수 없다.
2. W[X]를 제거한다.
3. W[X - 1] X W[X + 1] 만큼 에너지를 모은다.
4. N을 1 감소시키고, 에너지 구슬을 다시 1부터 N까지 번호를 매긴다.

N과 각 구슬의 에너지가 주어졌을 때, 모을 수 있는 에너지 양의 최대값을 구하라.

</br>

## 추가 사항

- 입력의 첫째 줄은 구슬의 개수 N (3 <= N <= 10)
- 입력의 둘째 줄은 각 구슬의 에너지를 공백으로 구분해서 주어짐 (1 <= W[i] <= 1000)

</br>

## 다른 사람의 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.StringReader;
import java.util.ArrayList;
import java.util.List;
import java.util.StringTokenizer;

public class Main {
	static BufferedReader input = new BufferedReader(new InputStreamReader(System.in));
	static StringTokenizer tokens;
	static int N, max = Integer.MIN_VALUE;

	public static void main(String[] args) throws NumberFormatException, IOException {
		N = Integer.parseInt(input.readLine());
		List<Integer> list = new ArrayList<>();
		tokens = new StringTokenizer(input.readLine());
		for(int n = 0; n < N; n++) {
			list.add(Integer.parseInt(tokens.nextToken()));
		}
		dfs(list, 0);
		System.out.println(max);
	}

	private static void dfs(List<Integer> list, int sum) {
		if(list.size() <= 2) {
			if(max < sum) {
				max = sum;
			}
			return;
		}

		for(int i = 1; i < list.size() - 1; i++) {
			int temp = list.get(i);
			int num = list.get(i - 1) * list.get(i + 1);
			list.remove(i);
			dfs(list, sum + num);
			list.add(i, temp);
		}
	}
}
```

main에서는 입력값을 받아오는 작업을 한 뒤, 전체 배열과 초기값 0을 가지고 재귀를 돌린다.  
재귀에서는 배열의 사이즈가 2가 될 때 max 값을 비교하며 list[i - 1] \* list[i + 1]의 값 중 최대값을 구하며 더해준다.  
최종적으로 그렇게 더해진 max 값을 출력해준다.  
뭔가 추상적으로는 이해가 되는데 list의 길이가 2가 될 때까지의 여정이 머릿속에 훤히 그려지지는 않는다.  
정리해두고 계속 보면서 작동 과정을 다시 확인해봐야겠다.

</br>

## 여담

[블로그 글](https://laugh4mile.tistory.com/68)을 통해서 다른 분의 풀이를 참조했다.  
Code States Hiring Assessment 평가가 다가오고 있는데, 재귀 문제를 꼭 다시 한번 확인해보라고 해서 Code States에서 제공해준 재귀 문제들을 다시금 풀어보고, 그래도 모자른 것 같아서 외부 사이트의 재귀 문제들을 찾던 중 이 문제를 발견했다.  
하지만 저번과 마찬가지로 입력값을 도대체 어떻게 받아와야 할지 난감해서 한참을 해매다가 결국엔 다른 분의 풀이를 참조하게 되었다.  
풀이를 참조해보니 Buffer Reader와 String Tokenonzer를 통해서 입력값을 받아오는 것을 확인할 수 있었다.  
앞으로도 백준 문제를 풀고 싶다면 이 두가지 키워드에 대해 꼭 공부해야겠다는 생각이 들었다.  
Code States의 HA2를 마치고 반드시 따로 사용법을 정리해봐야겠다.

</br>

많은 분들의 풀이를 확인해봤는데, 대부분이 메소드 명을 dfs라 적으시는 것을 보고 DFS 카테고리로 분류할까 생각도 해보았지만 백준 카테고리에 '재귀'라고 명시되어 있어서 그냥 재귀라는 카테고리로 적었다.  
DFS 문제들은 대부분 재귀를 활용해서 푼다고 하던데, 이 둘이 어떤 특징을 갖고 있는지, 구별점이 있다면 무엇이 있는지 꼼꼼히 정리해둬야겠다.
