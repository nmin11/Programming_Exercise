## **Programmers > 월간 코드 챌린지 시즌1 > 로또의 최고 순위와 최저 순위**

</br>

[연습 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/68935)

</br>

:books: 내가 사용한 프로그래밍 언어 : Java  
:roller_coaster: 난이도 : Level 1

</br>

## 문제 요약

자연수 n을 3진법으로 표현한 뒤, 이를 앞뒤로 뒤집어라.  
이후 뒤집어진 3진법 수를 다시 10진법으로 표현하여 리턴하라.

</br>

## 추가 사항

- 1 <= n <= 100,000,000 자연수

</br>

## 다른 사람의 풀이

고민을 해보았지만 3진법으로 어떻게 표현할 수 있을지 생각이 잘 안나서 [다른 사람의 풀이](https://jeleedev.tistory.com/35)를 참고했다.  
3진법 표현 방식만 알면 생각보다 간단한 문제이기도 하고 이해를 못했던 것은 또 아니지만, 이러한 연산 작용을 보다 확실하게 기억해두기 위해 이렇게 기록을 남기게 되었다.

```java
import java.util.ArrayList;
class Solution {
    public int solution(int n) {
        int answer = 0;
        ArrayList<Integer> temp = new ArrayList<>();

        // 10진법 -> 3진법(역순)
        while(true) {
            if(n < 3) { temp.add(n); break; }
            temp.add(n % 3);
            n = n / 3;
        }

        // 3진법(역순) -> 10진법
        for(int i = 0; i < temp.size(); i++) {
            answer += (Math.pow(3, temp.size() - i - 1) * temp.get(i));
        }

        return answer;
    }
}
```

필자는 3진법을 표현하기 위해 String을 써볼까 고민했지만(실제로 '다른 사람의 풀이' 탭에서 보니 나와 같은 생각을 한 사람들이 있기는 했었다.) 이 분은 ArrayList를 활용해서 3진법을 표현했다.  
1의 자리부터 시작해서 ArrayList의 값들을 담아주게 되기 때문에 자연스럽게 3진법을 역순으로 만들게 되었다.  
이렇게 해서 얻게 된 역순 3진법을 가지고, 각 자리수마다 (3의 제곱근 X 자리수)를 해주어서 10진법으로 다시 변환해주었다.  
String을 활용한 풀이도 복사해서 테스트를 돌려보았지만, 이쪽의 ArrayList를 사용하는 편이 테스트 통과 속도가 압도적으로 빨랐다.

</br>

## 소감

이로써 프로그래머스 Level 1문제들의 1페이지 문제들(20개)을 모두 풀 수 있었지만, 마지막 문제를 내 힘으로 직접 풀지 못해서 못내 찝찝하기는 하다.  
하지만 이렇게 직접 풀어내지 못한 문제 하나하나마다 자존심에 스크래치가 난다면, Algorithm 문제 풀이 자체를 오래 지속하지 못할 것이다.  
겸손한 마음으로 문제에 다가가며, 이 문제 풀이와 같이 앞으로의 Algorithm 문제 풀이에 도움이 될만한 풀이 방식이 있다면 반드시 여러 번 다시 보면서 확실히 내 것으로 만들어야겠다.
