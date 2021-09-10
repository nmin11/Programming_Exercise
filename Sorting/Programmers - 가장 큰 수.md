bㅠ## **Programmers > 정렬 > 가장 큰 수**

</br>

[연습 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42746)

</br>

📚 내가 사용한 프로그래밍 언어 : Java, JavaScript  
🎢 난이도 : Level 2

</br>

## 문제 요약

0 또는 양의 정수가 주어졌을 때, 정수를 이어 붙여 만들 수 있는 가장 큰 수를 알아내서 리턴하라.  
예를 들어, 주어진 정수가 [6, 10, 2]라면 [6102, 6210, 1062, 1026, 2610, 2106]을 만들 수 있고, 가장 큰 수는 6210이다.

</br>

## 추가 사항

- 1 <= numbers.length <= 100,000
- 0 <= numbers[i] <= 1,000
- return 타입은 문자열

</br>

## 다른 사람의 풀이 (Java)

```java
import java.util.Arrays;
import java.util.Comparator;

class Solution {
    public String solution(int[] numbers) {
        String[] result = new String[numbers.length];
        for (int i = 0; i < numbers.length; i++) {
            result[i] = String.valueOf(numbers[i]);
        }
        Arrays.sort(result, (el1, el2) -> (el2 + el1).compareTo(el1 + el2));

        if (result[0].equals("0")) {
            return "0";
        }

        StringBuilder sb = new StringBuilder();
        for (String el : result) {
            sb.append(el);
        }

        return sb.toString();
    }
}
```

나는 전혀 엉뚱한 방식으로 상당히 오랜 시간을 들여서 삽질을 했다.  
내가 Comparator 등을 활용한 정렬 방법을 너무 모르고 있었다는 생각이 들었다.  
반드시 시간을 들여서 공부를 해야만 하겠다.

</br>

## 다른 사람의 풀이 (JavaScript)

```javascript
function solution(numbers) {
  var answer = numbers
    .map((v) => v + "")
    .sort((a, b) => (b + a) * 1 - (a + b) * 1)
    .join("");

  return answer[0] === "0" ? "0" : answer;
}
```
