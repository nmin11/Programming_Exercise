## **Programmers > 스택/큐 > 기능개발**

</br>

[연습 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42586)

</br>

:books: 내가 사용한 프로그래밍 언어 : Java, JavaScript  
:roller_coaster: 난이도 : Level 2

</br>

## 문제 요약

프로그래머스 팀에서는 기능 개선 작업을 수행 중이다.  
각 기능은 진도가 100%일 때 서비스에 반영할 수 있다.  
각 기능의 개발 속도는 모두 다르기 때문에 뒤에 있는 기능이 앞에 있는 기능보다 먼저 개발될 수 있고, 이때 뒤에 있는 기능은 앞에 있는 기능이 배포될 때 함께 배포된다.  
먼저 배포되어야 하는 순서대로 작업의 진도가 적힌 정수 배열 progresses와 각 작업의 개발 속도가 적힌 정수 배열 speeds가 주어질 때 각 배포마다 몇 개의 기능이 배포되는지를 return하도록 soloution 함수를 완성하라.

</br>

## 추가 사항

- 작업의 개수는 100개 이하
- 작업 진도는 100 미만의 자연수
- 작업 속도는 100 이하의 자연수
- 배포는 하루에 한 번만

</br>

## 내 풀이

```java
import java.util.*;

class Solution {
    public int[] solution(int[] progresses, int[] speeds) {
        List<Integer> answer = new ArrayList<Integer>();
        int biggerIdx = 0;
        int count = 0;
        int temp = 0;

        while(progresses.length != temp) {
            for (int i = temp; i < progresses.length; i++) {
                progresses[i] += speeds[i];
            }
            for (int i = temp; i < progresses.length; i++) {
                if (progresses[i] >= 100) {
                    biggerIdx++;
                } else {break;}
            }
            if (count < biggerIdx) {
                count = biggerIdx;
                answer.add(count);
                count = 0;
            }
            temp += biggerIdx;
            biggerIdx = 0;
        }

        int[] array = new int[answer.size()];
        int size = 0;
        for(int el : answer){
          array[size++] = el;
        }

        return array;
    }
}
```

Code States의 코플릿 문제 중 하나가 이와 비슷했다는 점을 깨닫고 풀게 된 문제였던 만큼, 풀이도 코플릿에서 했던 풀이와 비슷한 방식으로 나왔다.  
하지만 다른 사람의 풀이를 보니 Java에서는 이미 Stack이나 Queue에 관련된 타입을 따로 제공해준다는 점을 깨닫게 되었다.

</br>

## 다른 사람의 풀이

```java
import java.util.*;

class Solution {
    public int[] solution(int[] progresses, int[] speeds) {
        Queue<Integer> q = new LinkedList<>();
        List<Integer> answerList = new ArrayList<>();

        for (int i = 0; i < speeds.length; i++) {
            double remain = (100 - progresses[i]) / (double) speeds[i];
            int date = (int) Math.ceil(remain);

            if (!q.isEmpty() && q.peek() < date) {
                answerList.add(q.size());
                q.clear();
            }

            q.offer(date);
        }

        answerList.add(q.size());

        int[] answer = new int[answerList.size()];

        for (int i = 0; i < answer.length; i++) {
            answer[i] = answerList.get(i);
        }

        return answer;
    }
}
```

사실 Queue의 활용도 그렇지만 연산 과정이 꽤나 인상 깊다.  
하지만 아무래도 아직 나는 Queue를 활용해 본 적이 없다보니 이는 Queue 타입을 조금 더 공부하고 나서 이해해도 늦지 않겠다는 생각이 든다.  
Queue는 추후에 꼭 학습을 해서 TIL에 정리해보도록 하자.

</br>

※ 참고로 JavaScript 풀이는 Java 풀이와 상당히 비슷하게 제출하여 따로 옮겨 적지는 않았다.
