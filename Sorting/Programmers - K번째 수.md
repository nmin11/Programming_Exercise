## **Programmers > 정렬 > K번째 수**

</br>

[연습 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42748)

</br>

:books: 내가 사용한 프로그래밍 언어 : Java, JavaScript  
:roller_coaster: 난이도 : Level 1

</br>

## 문제 요약

array의 i번째 숫자부터 j번째 숫자까지 자르고 정렬했을 때, k번째에 있는 수를 구한다.  
array, [i, j, k]를 원소로 가진 2차원 배열 commands가 매개변수로 주어질 때, commands의 모든 원소에 대해 앞서 설명한 연산을 적용했을 때 나온 결과를 배열에 담아 return 하도록 함수를 작성하라.

</br>

## 추가 사항

- array의 길이는 1 이상 100 이하
- array의 각 원소는 1 이상 100 이하
- commands의 길이는 1 이상 50 이하
- commands의 각 원소는 길이가 3

</br>

## Java 풀이

```java
import java.util.Arrays;

class Solution {
    public int[] solution(int[] array, int[][] commands) {
        int[] answer = new int[commands.length];

        for (int i = 0; i < commands.length; i++) {
            int[] slicedArr = Arrays.copyOfRange(array, commands[i][0] - 1, commands[i][1]);
            Arrays.sort(slicedArr);
            answer[i] = slicedArr[commands[i][2] - 1];
        }
        return answer;
    }
}
```

사실 처음에 배열에 요소들을 어떻게 넣어야 할지 몰라서 항상 익숙하게 사용해 왔던 ArrayList를 활용해 보기 위해서 answer를 ArrayList로 바꿔서 연산을 해보았지만 배열과 ArrayList 간의 변환이 원활하게 이루어지지 않았다.  
하지만 구글링을 좀 해보니, ArrayList까지 갈 필요가 없었고 배열의 길이를 딱 정해놓고 사용해도 충분한 것이었다. :open_mouth:  
아직도 배열을 사용하는 것에 익숙하지 않다는 사실을 깨달았다.  
그리고 Arrays의 copyOfRange라는 메소드도 처음 알게 되었지만 JavaScript의 slice와 유사한 용도로 보여서 사용하는 데에 크게 어려움을 느끼진 않았다.  
copyOfRange에 대해서 간단하게 정리하자면, 첫번째 인자로 복사할 배열을 넣고, 두번째 인자로 복사를 시작할 인덱스를 넣고, 세번째 인자로 배열의 어디까지 복사할 것인지 해당 배열의 인덱스를 넣어준다.  
그러면 간단하게 복사가 되고 변수에 할당해줄 수 있게 된다.

</br>

## JavaScript 풀이

```javascript
function solution(array, commands) {
  var answer = [];
  let slicedArr = [];

  for (let i = 0; i < commands.length; i++) {
    slicedArr = array.slice(commands[i][0] - 1, commands[i][1]);
    slicedArr.sort((a, b) => a - b);
    answer.push(slicedArr[commands[i][2] - 1]);
  }

  return answer;
}
```

역시 JavaScript로도 풀어보니 금방 답을 도출해낼 수 있었다.  
다만 조금 헷갈렸던 부분이 sort((a, b) => a - b); 부분이었는데, 이는 숫자들도 문자열 기준에 따라 정렬되기 때문에 이런 화살표 함수를 적용해 준 것이다.

</br>

## 소감

이 문제를 처음 봤을 때, '이 문제 쉽겠는데?' 하는 생각이 들었고, 정말로 쉬운 문제가 맞았다.  
하지만 배열의 사용이 익숙치 않아서 애를 먹었고 copOfRange도 처음 사용해보는 메소드였다.  
그만큼 아직도 기본기가 부족하다는 뜻이다.  
그리고 뭔가 JavaScript에서 배열을 다루는 편이 뭔가 더 익숙한 느낌이다.  
이는 아무래도 Java로 문제 풀이를 많이 해보지 않아서 그런 것 같다.
