## **Programmers > 2021 Dev-Matching > 로또의 최고 순위와 최저 순위**

</br>

[연습 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/77484)

</br>

:books: 내가 사용한 프로그래밍 언어 : Java, JavaScript  
:roller_coaster: 난이도 : Level 1

</br>

## 문제 요약

로또 6/45는 1부터 45까지의 숫자 중 6개를 찍어서 맞히는 대표적인 복권이다.  
로또를 구매한 민우는 동생이 로또에 낙서를 하는 바람에 로또의 일부 번호를 알아볼 수 없게 되었다.  
당첨 번호 발표 후, 민우는 자신이 구매했던 로또의 당첨이 가능했던 최고 순위와 최저 순위를 알아보고 싶어졌다.  
알아볼 수 없게 된 번호를 0으로 표기하고서, 0이 어떤 숫자가 되었을 때 최고 순위가 되고, 또 어떤 숫자가 되었을 때 최저 순위가 되는지 그 순위들을 배열에 담아서 리턴해라.

</br>

## 추가 사항

- 순서와 상관없이, 구매한 로또에 당첨 번호와 일치하는 번호가 있으면 맞힌 걸로 인정
- lottos는 길이 6인 정수 배열
- lottos의 모든 원소는 0 이상 45 이하인 정수
  - 0을 제외한 다른 숫자들이 중복으로 담겨있는 경우는 없음
- win_nums는 길이 6인 정수 배열
- win_nums의 모든 원소는 1 이상 45 이하인 정수
  - win_nums에도 같은 숫자가 중복으로 담겨있지 않음

</br>

## 내 풀이 (Java)

```java
class Solution {
    public int[] solution(int[] lottos, int[] win_nums) {
        int correct = 0;
        int zeroNums = 0;

        for (int i = 0; i < win_nums.length; i++) {
            for (int j = 0; j < lottos.length; j++) {
                if (lottos[j] == win_nums[i]) {
                    correct++;
                    break;
                }
            }
        }

        for (int l : lottos) {
            if (l == 0) zeroNums++;
        }

        int maxRank = 7 - (correct + zeroNums);
        int minRank = 7 - correct;
        if (maxRank > 6) maxRank = 6;
        if (minRank > 6) minRank = 6;

        return new int[] {maxRank, minRank};
    }
}
```

이실직고를 하자면, 온전히 내 힘으로 테스트를 통과하고 제출에는 성공했지만, 제출했던 코드는 이보다 좀 더 복잡했다. (단순한 사칙 연산 코드들이 지나치게 길었다.)  
이후 '다른 사람의 풀이'를 참조하여 연산하는 부분만 조금 줄였으니 양해를 부탁한다.  
간단한 문제였던 만큼 풀이도 간단하다.  
lottos와 win_nums를 비교해서 겹치는 부분이 있으면 correct에 1씩 더해준다.  
그리고 lottos만 따로 검사해서 0이 있으면 zeroNums에 1씩 더해준다.  
이렇게 해서 나온 correct와 zeroNums를 가지고 간단히 연산해주면 되는 문제였다.

</br>

## 다른 사람의 풀이 (Java)

```java
import java.util.HashMap;
import java.util.Map;

class Solution {
    public int[] solution(int[] lottos, int[] win_nums) {
        Map<Integer, Boolean> map = new HashMap<Integer, Boolean>();
        int zeroCount = 0;

        for(int lotto : lottos) {
            if(lotto == 0) {
                zeroCount++;
                continue;
            }
            map.put(lotto, true);
        }


        int sameCount = 0;
        for(int winNum : win_nums) {
            if(map.containsKey(winNum)) sameCount++;
        }

        int maxRank = 7 - (sameCount + zeroCount);
        int minRank = 7 - sameCount;
        if(maxRank > 6) maxRank = 6;
        if(minRank > 6) minRank = 6;

        return new int[] {maxRank, minRank};
    }
}
```

map을 활용해서 조금 더 깔끔하게 sameCount와 zeroCount를 추려냈다는 것이 인상적이었다.  
나는 map의 활용이 익숙하지 않다보니 이런 풀이를 아예 생각조차 못한다는 사실이 부끄럽다.  
언제라도 꼭 시간을 내서 Java의 기본 클래스들을 확실히 익혀놔야겠다.

</br>

## 다른 사람의 풀이 (Java 람다식 활용)

```java
import java.util.Arrays;
import java.util.stream.LongStream;

class Solution {
    public int[] solution(int[] lottos, int[] winNums) {
        return LongStream.of(
            (lottos.length + 1) - Arrays.stream(lottos).filter(l -> Arrays.stream(winNums).anyMatch(w -> w == l) || l == 0).count(),
            (lottos.length + 1) - Arrays.stream(lottos).filter(l -> Arrays.stream(winNums).anyMatch(w -> w == l)).count()
        )
            .mapToInt(op -> (int) (op > 6 ? op - 1 : op))
            .toArray();
    }
}
```

사실 람다식은 진짜 보기만 해도 어안이 벙벙해지고 뭐가 뭔지 모르겠다.  
그리고 위의 코드는 작업 처리 과정이 느리다.  
하지만 람다식의 활용 방법은 나중에라도 꼭 학습해볼 것이기 때문에 이렇게 옮겨적게 되었다.

</br>

## 내 풀이 (JavaScript)

```javascript
function solution(lottos, win_nums) {
  var answer = [];

  let correct = 0;
  let zeroNums = 0;

  for (let i of lottos) {
    if (i === 0) {
      zeroNums++;
      continue;
    }
    for (let j of win_nums) {
      if (i === j) correct++;
    }
  }

  answer.push(getGrade(correct + zeroNums));
  answer.push(getGrade(correct));

  return answer;
}

const getGrade = function (num) {
  switch (num) {
    case 6:
      return 1;
    case 5:
      return 2;
    case 4:
      return 3;
    case 3:
      return 4;
    case 2:
      return 5;
    default:
      return 6;
  }
};
```

JavaScript는 사실 온전한 내 풀이가 아니다.  
이 문제의 해결에 다가가기 위해서 어떠한 로직이 필요할지 이미 알게 되었다 보니, 시간 절약을 위해서 Java의 다른 사람 풀이(위쪽에 첨부한 코드와는 별개의 코드)를 참고해서 JavaScript 방식으로 풀어보았다.

</br>

## 다른 사람의 풀이 (JavaScript)

```javascript
function solution(lottos, win_nums) {
  const rank = [6, 6, 5, 4, 3, 2, 1];

  let minCount = lottos.filter((v) => win_nums.includes(v)).length;
  let zeroCount = lottos.filter((v) => !v).length;

  const maxCount = minCount + zeroCount;

  return [rank[maxCount], rank[minCount]];
}
```

코드가 간결하면서 성능 이슈도 없다.  
그리고 내가 다 아는 메소드들이다.  
하지만 이런 코드는 상상해낼 수 없었던 자신을 반성해보며 이렇게 옮겨적어 보았다.
