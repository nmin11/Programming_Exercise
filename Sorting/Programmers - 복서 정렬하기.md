## **Programmers > 위클리 챌린지 6주차 > 복서 정렬하기**

</br>

[연습 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/85002)

</br>

📚 내가 사용한 프로그래밍 언어 : Java  
🎢 난이도 : Level 1

</br>

## 문제 요약

복서 선수들의 몸무게 weights와, 복서 선수들의 전적을 나타내는 head2head가 매개변수로 주어진다.  
복서들의 번호를 다음과 같은 순서로 정렬하고 리턴하라

1. 전체 승률이 높은 복서의 번호가 앞쪽으로 간다.  
   한번도 싸운 적이 없는 복서의 승률은 0%로 취급한다.
2. 승률이 동일하다면 자신보다 몸무게가 무거운 복서를 이긴 횟수가 많은 복서의 번호가 앞쪽으로 간다.
3. 자신보다 무거운 복서를 이긴 횟수마저 동일하다면 자기 몸무게가 무거운 복서의 번호가 앞쪽으로 간다.
4. 자기 몸무게까지 동일하다면 더 작은 번호가 앞쪽으로 간다.

</br>

## 추가 사항

1. 2 <= weights.length <= 1,000
   - 45 <= weights[i] <= 150, 정수, i+1번 복서의 몸무게를 의미
2. head2head.length = weights.length
   - head2head[i].length() = weights.length
   - head2head[i]는 'N', 'W', 'L'로 이루어진 문자열, i+1번 복서의 전적을 의미
   - head2head[i][j]는 i+1번 복서와 j+1번 복서의 매치 결과
     - 'N' (None)은 두 복서가 아직 붙어본 적이 없음을 의미
     - 'W' (Win)은 i+1번 복서가 j+1번 복서를 이겼음을 의미
     - 'L' (Lose)는 i+1번 복서가 j+1번 복서에게 졌음을 의미
   - 자기 자신과 싸울 수 없기 때문에 head2head[i][i]는 항상 'N'

</br>

## 다른 사람의 풀이 (Java)

```java
import java.util.List;
import java.util.ArrayList;

class Solution {
    class Boxer {
        int num;
        int weight;
        int winCount;
        int fightCount;
        int winOverWeightCount;
        double winRate;

        public Boxer(int num, int weight) {
            this.num = num;
            this.weight = weight;
            this.winCount = 0;
            this.fightCount = 0;
            this.winOverWeightCount = 0;
        }
    }

    public int[] solution(int[] weights, String[] head2head) {
        int len = weights.length;
        List<Boxer> boxers = new ArrayList<>();

        for (int i = 0; i < len; i++) {
            boxers.add(new Boxer(i + 1, weights[i]));
        }

        for (int i = 0; i < len; i++) {
            for (int j = 0; j < len; j++) {
                if (head2head[i].charAt(j) != 'N') {
                    boxers.get(i).fightCount++;
                }
                if (head2head[i].charAt(j) == 'W') {
                    boxers.get(i).winCount++;
                    if (boxers.get(j).weight > boxers.get(i).weight) {
                        boxers.get(i).winOverWeightCount++;
                    }
                }
            }
        }

        boxers.stream().forEach(el -> {
            if (el.fightCount > 0) {
                el.winRate = (double) el.winCount / el.fightCount;
            }
        });

        boxers.sort((a, b) -> {
            if (a.winRate != b.winRate) {
                return (b.winRate - a.winRate) > 0 ? 1 : -1;
            } else if (a.winOverWeightCount != b.winOverWeightCount) {
                return b.winOverWeightCount - a.winOverWeightCount;
            } else if (a.weight != b.weight) {
                return b.weight - a.weight;
            } else {
                return a.num - b.num;
            }
        });

        return boxers.stream().mapToInt(el -> el.num).toArray();
    }
}
```

Level 1 문제임에도 꽤나 로직이 복잡하겠다는 느낌이 들었고, 어느 정도 풀어보다가 한번 수틀리자 그냥 유용한 풀이를 보고 잘 참고해보기로 했다.  
여러가지 풀이들을 검색해봤는데 이 풀이가 정말 깔끔하고 이해도 잘 되었다.  
class를 사용하여 아주 손쉽게 정렬하는 과정이 특히 인상 깊었다.  
다음에는 이런 비슷한 유형의 문제들을 꼭 잘 풀어낼 수 있도록 하자.
