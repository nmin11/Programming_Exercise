## **Programmers > 완전탐색 > 모의고사**

</br>

[연습 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42840)

</br>

📚 내가 사용한 프로그래밍 언어 : JavaScript  
🎢 난이도 : Level 1

</br>

## 문제 요약

수포자(수학을 포기한 사람) 삼인방은 모의고사에 수학 문제를 전부 찍으려 한다.  
수포자는 모든 문제를 다음과 같이 찍는다.

- 1번 수포자 : 1, 2, 3, 4, 5, 1, 2, 3, 4, 5, ...
- 2번 수포자 : 2, 1, 2, 3, 2, 4, 2, 5, 2, 1, 2, 3, 2, 4, 2, 5, ...
- 1번 수포자 : 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, ...

모든 문제의 정답이 순서대로 들어 있는 배열 answers가 주어졌을 때, 가장 많은 문제를 맞힌 사람이 누구인지 배열에 담아 return하라.

</br>

## 추가 사항

- 시험은 최대 10,000 문제
- 문제의 정답은 1, 2, 3, 4, 5 중 하나
- 가장 높은 점수를 받은 사람이 여럿일 경우, return하는 값을 오름차순으로 정렬할 것

</br>

## 내 풀이

```javascript
function solution(answers) {
  var answer = [];

  let a = 0;
  let b = 0;
  let c = 0;

  for (let i = 0; i < answers.length; i++) {
    if (i % 5 === 0 && answers[i] === 1) {
      a++;
    } else if (i % 5 === 1 && answers[i] === 2) {
      a++;
    } else if (i % 5 === 2 && answers[i] === 3) {
      a++;
    } else if (i % 5 === 3 && answers[i] === 4) {
      a++;
    } else if (i % 5 === 4 && answers[i] === 5) {
      a++;
    }
  }

  for (let i = 0; i < answers.length; i++) {
    if (i % 2 === 0 && answers[i] === 2) {
      b++;
    } else {
      if (i % 8 === 1 && answers[i] === 1) {
        b++;
      } else if (i % 8 === 3 && answers[i] === 3) {
        b++;
      } else if (i % 8 === 5 && answers[i] === 4) {
        b++;
      } else if (i % 8 === 7 && answers[i] === 5) {
        b++;
      }
    }
  }

  for (let i = 0; i < answers.length; i++) {
    if ((i % 10 === 0 || i % 10 === 1) && answers[i] === 3) {
      c++;
    } else if ((i % 10 === 2 || i % 10 === 3) && answers[i] === 1) {
      c++;
    } else if ((i % 10 === 4 || i % 10 === 5) && answers[i] === 2) {
      c++;
    } else if ((i % 10 === 6 || i % 10 === 7) && answers[i] === 4) {
      c++;
    } else if ((i % 10 === 8 || i % 10 === 9) && answers[i] === 5) {
      c++;
    }
  }

  if (a > b && a > c) {
    answer.push(1);
  } else if (b > a && b > c) {
    answer.push(2);
  } else if (c > a && c > b) {
    answer.push(3);
  } else {
    if (a === b && a > c) {
      answer.push(1);
      answer.push(2);
    } else if (a === c && a > b) {
      answer.push(1);
      answer.push(3);
    } else if (b === c && b > a) {
      answer.push(2);
      answer.push(3);
    } else if (a === b && b === c && a === c) {
      answer.push(1);
      answer.push(2);
      answer.push(3);
    }
  }

  return answer;
}
```

스스로 문제를 풀면서도 1차원적으로 풀고 있다는 느낌을 많이 받았다.  
계속해서 이런 식으로 문제를 풀어가게 된다면 더 높은 수준으로 올라가지 못할 것이라는 생각이 든다.

</br>

## 다른 사람의 풀이

```javascript
function solution(answers) {
  var answer = [];
  var a1 = [1, 2, 3, 4, 5];
  var a2 = [2, 1, 2, 3, 2, 4, 2, 5];
  var a3 = [3, 3, 1, 1, 2, 2, 4, 4, 5, 5];

  var a1c = answers.filter((a, i) => a === a1[i % a1.length]).length;
  var a2c = answers.filter((a, i) => a === a2[i % a2.length]).length;
  var a3c = answers.filter((a, i) => a === a3[i % a3.length]).length;
  var max = Math.max(a1c, a2c, a3c);

  if (a1c === max) {
    answer.push(1);
  }
  if (a2c === max) {
    answer.push(2);
  }
  if (a3c === max) {
    answer.push(3);
  }

  return answer;
}
```

분명 내가 모르는 메소드가 없음에도 이해하는 데에 시간이 걸렸다.  
이해한 바를 말해보자면, filter 메소드 안의 비교 대상을 a[i % a.length]로 잡아줬는데, 여기서 %는 내가 5로 나눴을 때의 나머지, 8로 나눴을 때의 나머지, 10으로 나눴을 때의 나머지를 하나하나 비교한 것과 똑같은 작용을 한다.  
이렇게 filter된 배열의 길이를 바로 변수에 담아줬기 때문에 각 수포자들의 점수를 깔끔하게 가려낼 수 있다.  
Math.max를 활용하여 최댓값을 구한 것도 코드를 효과적으로 줄여주는 데에 한 몫 했다.

</br>

## 다른 사람의 풀이 (Java)

```java
import java.util.*;

class Solution {
    public static int[] solution(int[] answers) {
        int[][] patterns = {
                {1, 2, 3, 4, 5},
                {2, 1, 2, 3, 2, 4, 2, 5},
                {3, 3, 1, 1, 2, 2, 4, 4, 5, 5}
        };

        int[] hit = new int[3];
        for(int i = 0; i < 3; i++) {
            for(int j = 0; j < answers.length; j++) {
                if(patterns[i][j % patterns[i].length] == answers[j]) hit[i]++;
            }
        }

        int max = Math.max(hit[0], Math.max(hit[1], hit[2]));
        List<Integer> list = new ArrayList<>();
        for(int i = 0; i < hit.length; i++)
            if(max == hit[i]) list.add(i + 1);

        int[] answer = new int[list.size()];
        int cnt = 0;
        for(int num : list)
            answer[cnt++] = num;
        return answer;
    }
}
```

로직이 상당히 인상 깊었다.  
솔직히 이런 접근 방식을 봐두고 다시 활용하라고 하면 무리겠다는 생각이 들지만, 여러 번 참고하면서 조금이라도 이런 로직을 짜는 방법에 더 익숙해지고자 한다.

</br>

## 소감

오늘 프로그래머스의 문제들 여러 개를 기웃거렸지만 손쉽게 풀리는 문제가 없었다.  
그나마 이 문제를 풀 수 있었지만 스스로의 풀이 방식이 참 아쉽다.  
문제 풀이에 관련된 영상이나 강의들을 조금 참조해야 될 것 같기도 하다.

</br>

더불어서, 내 본진이라고 할 수 있었던 Java를 활용해서 문제를 푸는 것이 까다롭게 느껴지기 시작했다.  
배열을 다루는 부분에서는 JavaScript를 활용하는 편이 더 간단하다는 점을 깨달은 것이다.  
요새 문제를 풀 때 Java와 JavaScript, 두개를 번갈아 가면서 활용했는데, 나중에 진짜로 코딩 테스트를 볼 때 어떤 언어를 활용해야 할지 고민이 된다.  
일단은 가능하면 두 가지 언어로 다 문제를 풀어볼 수 있도록 해봐야겠다.  
시간은 더 오래 걸리겠지만 다다익선이라고 생각한다.
